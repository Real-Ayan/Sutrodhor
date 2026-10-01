# Sutrodhor

**Sutrodhor** is a native, AI-assisted writing and research environment.

> **A native writing environment where research becomes structured context for the writing itself.**

It connects **ideas, claims, sources, evidence, and drafts** so writers can understand not only what they are writing, but where the ideas and information behind it came from.

> **From sources to story.**

**Ideas → Claims → Sources → Evidence → Outline → Draft → Fact Check → Story**

---

## What it does

Sutrodhor aims to bring writing and research into one focused workspace.

* Markdown-first writing environment
* Research and source collection
* Ideas and claim tracking
* Evidence and citation management
* AI-assisted research and writing
* Fact-checking and claim verification
* Research and story graphs
* Workflows for scripts, essays, and nonfiction
* Local-first project storage
* Native desktop application (Linux first)

The goal isn't simply to have AI write for you.

It's to help you **research, understand, organize, verify, and then write**.

---

## Why Sutrodhor?

**সূত্রধর (Sutrodhor)** is a Bengali word traditionally associated with a narrator or storyteller who helps carry and connect a narrative.

The name also evokes **সূত্র (sutro)** — a thread, connection, or source.

That reflects the central idea of the project: connecting the many threads behind a piece of writing.

Product UI and code stay in English. The name origin is the one place non-English belongs on purpose.

---

## The idea

AI is already very good at generating text.

Sutrodhor explores a different question:

> **What if the writing environment understood the research behind the writing?**

Instead of treating a document as a blank page, Sutrodhor treats it as a network of ideas, claims, sources, evidence, and stories.

> **The document is not the database. The document is one view of the writer's knowledge.**

---

## Architecture

```text
┌─────────────────────────────┐
│        Desktop UI           │
│       Tauri + React         │
└──────────────┬──────────────┘
               │
        ┌──────▼──────┐
        │    Rust     │
        │             │
        │ Core        │
        │ Documents   │
        │ Storage     │
        │ Graph       │
        │ Search      │
        └──────┬──────┘
               │
        ┌──────▼──────┐
        │   Python    │
        │   FastAPI   │
        │             │
        │ AI / Agents │
        │ Research    │
        │ Fact Check  │
        └─────────────┘
```

Rust owns the application, documents, project state, storage, search, and graph.

Python provides AI, research, and agent capabilities.

They talk over local HTTP + OpenAPI — not shared memory, not one mega-process.

| Layer | Choice | Owns |
| --- | --- | --- |
| Desktop shell | Tauri v2 + Rust | App state, filesystem, documents, future SQLite, search, jobs, calls to AI |
| UI | React + TypeScript + Vite | Editor, panels, interactions, visualizations |
| Editor (later) | CodeMirror 6 | Markdown editing |
| AI service | FastAPI + Pydantic + uv | LLM, research agents, extraction, fact check (stubs first) |
| Target OS | Linux first | `cargo tauri dev` now; AppImage later |

More detail: [docs/architecture.md](docs/architecture.md).

---

## Project status

**Early development.** Sutrodhor is a learning project and an exploration of what a research-aware, agentic writing environment could look like.

Right now: **docs and roadmap only.** No desktop binary or AI server yet.

Next build slice: empty app stubs → FastAPI `GET /health` → Tauri three-pane shell → project/document filesystem workflow.

See [docs/roadmap.md](docs/roadmap.md) for phases and stop lines.

---

## Repository layout (target)

Repo folder stays **`Sutrodhor`**. Package/crate names use lowercase **`sutrodhor`**.

```text
Sutrodhor/
├── apps/
│   ├── desktop/          # Tauri + React (sutrodhor-desktop) — not created yet
│   └── ai-server/        # FastAPI (sutrodhor-ai) — not created yet
├── docs/
│   ├── architecture.md
│   ├── domain-model.md
│   ├── roadmap.md
│   ├── monorepo.md
│   ├── learning-path.md
│   ├── working-agreement.md
│   └── todo/             # phase-by-phase checklists
├── README.md
└── .gitignore
```

Details: [docs/monorepo.md](docs/monorepo.md).

---

## How to run

**TODO — apps do not exist yet.**

When they do:

```bash
# AI service health (planned)
cd apps/ai-server && uv run uvicorn app.main:app --reload

# Desktop (planned, Linux)
cd apps/desktop && npm install && npm run tauri dev
```

Until then, follow [docs/todo/phase-1-writer.md](docs/todo/phase-1-writer.md).

---

## Documentation

| Doc | What it is |
| --- | --- |
| [docs/architecture.md](docs/architecture.md) | Why Rust vs Python, filesystem, future SQLite, boundaries |
| [docs/domain-model.md](docs/domain-model.md) | Idea, Claim, Source, Evidence, Document, Relationship |
| [docs/roadmap.md](docs/roadmap.md) | Phases 1–5 with stop lines |
| [docs/todo/](docs/todo/) | Ordered tasks per phase |
| [docs/monorepo.md](docs/monorepo.md) | Two languages in one repo |
| [docs/learning-path.md](docs/learning-path.md) | What to learn before each phase |
| [docs/working-agreement.md](docs/working-agreement.md) | How guide + co-implement works |

---

## License

TBD. For a public GitHub repo, **MIT** is the simple default when you are ready to add one.
