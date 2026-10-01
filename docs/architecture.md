# Architecture

Opinionated guide for how Sutrodhor is shaped. Read this before adding folders or dependencies.

---

## The core idea

A writing tool usually treats the **document** as the center of the universe. Sutrodhor does not.

The document is a **view** over structured knowledge: ideas, claims, sources, evidence, and the relationships between them. Markdown files on disk remain real and editable. They are not the only model of truth for research.

That split is why the architecture has two runtimes and a clear filesystem layout.

---

## Two processes, one product

```text
                 Sutrodhor
                     │
          ┌──────────┴──────────┐
          │                     │
       Rust App              Python AI
     (Tauri desktop)      (FastAPI sibling)
          │                     │
   Project / Documents      LLM / Agents
   Files / Storage          Research
   Search / Graph           Fact checking
   Native UI host           Extraction
```

### Why Rust owns the application

The desktop app must be trustworthy with **your files and project state**.

Rust (via Tauri) should eventually own:

- application and project state
- filesystem create/open/save
- document metadata and IDs
- persistence and future SQLite index
- search / indexing
- graph / domain model in-process
- background jobs
- calling the AI layer over HTTP

React/TypeScript owns the **UI**: layout, editor surface, panels, command palette, visualizations. It should not become the place where project rules and storage logic live. If a rule matters when the UI is closed, it belongs in Rust.

### Why Python is a separate AI service

Python is where LLM ecosystems, research scripts, and extraction libraries are easiest. Keep that world in `apps/ai-server`.

Python should **not** own:

- which project is open
- where documents live
- the authoritative document text
- the long-term graph of record (that stays with the app / SQLite later)

Think: **Rust is the application. Python is intelligence on request.**

FastAPI + Pydantic give you a clear HTTP boundary and schemas from day one. Typer can appear later as a CLI wrapper around the same logic; it is not a substitute for the local HTTP service the desktop will call.

---

## Filesystem is the source of truth for documents

A user project will look roughly like:

```text
my-project/
├── project.toml
├── documents/
│   ├── script.md
│   └── notes.md
├── sources/          # later
├── research/         # later
└── .sutrodhor/
    └── (empty for now; later: index.sqlite, caches)
```

Rules for the early product:

1. **Create / open project** creates or reads this tree.
2. **Create / edit / save document** writes Markdown under `documents/`.
3. **`.sutrodhor/` exists** from project creation, even if empty — reserve the app-private space early.
4. Document identity uses a **UUID** in metadata (and/or `project.toml` mapping), while the **file on disk** remains what you can open in any editor.

Do not pretend SQLite is the document store. Writers must be able to recover text from `.md` files if the index burns down.

---

## Future SQLite: index and graph cache

Later, under `.sutrodhor/index.sqlite` (name can evolve):

- search index over documents and sources
- claim / evidence / relationship tables
- caches that make the research panel fast

SQLite is a **derived and structured layer**, rebuilt or updated from filesystem + explicit research objects. If you ever feel tempted to store the only copy of a draft only in SQLite — stop.

---

## UI ↔ research data flow (intended)

```text
┌────────────┐   Tauri commands    ┌─────────────────┐
│ React UI   │ ──────────────────► │ Rust app core   │
│ editor     │ ◄────────────────── │ project, docs   │
│ tree       │   state / events    │ FS, later SQLite│
│ context    │                     │                 │
└────────────┘                     └────────┬────────┘
                                            │ HTTP + OpenAPI
                                            ▼
                                   ┌─────────────────┐
                                   │ Python AI       │
                                   │ /chat, /research│
                                   │ placeholders →  │
                                   │ real agents     │
                                   └─────────────────┘
```

The right-hand **Context** panel (Research, Claims, Sources, Evidence) starts as static placeholders. When it becomes real:

1. UI asks Rust for structured context for the open project / selection.
2. Rust reads FS + SQLite (later) and returns typed data.
3. When the user runs an AI action, Rust calls Python, then **persists results** it cares about; Python does not become the database.

---

## Domain direction (types, not a full DB yet)

Prefer explicit Rust types over stringly maps when you start coding:

- `ProjectId`, `DocumentId`, `SourceId`, `ClaimId`, `EvidenceId`, `IdeaId`
- structs/enums for `Project`, `Document`, and later `Claim`, `Source`, `Evidence`, `Relationship`

Use `Result` and proper errors. Panic only for true programmer bugs.

See [domain-model.md](domain-model.md) for the conceptual model.

---

## Principles

1. **Do not over-engineer.** No microservices fleet, Redis, Kafka, vector DB, graph DB product, auth cloud, or plugin marketplace in Phase 1–2.
2. **Boring architecture wins.** Explicit folders, explicit commands, minimal dependencies.
3. **No fake functionality.** A panel that says “Coming soon” is honest. A fake research agent that pretends to work is not.
4. **Stop lines exist.** Finish a milestone; do not “while we’re here” the next phase.
5. **Teach in docs, keep code calm.** Prefer mentor writing here over dense tutorial comments in every Rust file.
6. **Linux first.** Get `cargo tauri dev` solid on Linux before packaging (AppImage) or other OSes.

---

## What “done” looks like for the foundation

You can:

1. Run the desktop app on Linux.
2. Create/open a project directory.
3. Create, edit, save Markdown; reopen and see it again.
4. See the three-pane UI with a placeholder context panel.
5. Run the Python service and hit `GET /health`.

Anything beyond that waits for an explicit phase task in [roadmap.md](roadmap.md) and [todo/](todo/).
