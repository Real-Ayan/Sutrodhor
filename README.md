# Sutrodhor

> A native writing environment where research becomes structured context for the writing itself.

Sutrodhor is a Linux-first, AI-assisted writing and research desktop application. The long-term idea is to connect:

**Ideas → Claims → Sources → Evidence → Outline → Draft → Fact Check → Story**

The document is not the database. The document is one view of the writer's knowledge.

This is an early-stage personal/learning product. The foundation is being built in public; the full product is not here yet.

---

## Name

**Sutrodhor** (সূত্রধর) — from Bangla/Sanskrit roots. A *sutradhar* is traditionally the narrator or thread-holder of a play: the one who holds the *sutra* (thread) of the story. That metaphor fits: you hold research, claims, and evidence as threads, then weave them into writing.

Product UI and code comments stay in English. The name origin is the one place non-English belongs on purpose.

---

## Status

**Docs and roadmap only.** No desktop binary or AI server yet.

Next build slice (when we start coding): empty app stubs → FastAPI `GET /health` → Tauri three-pane shell → project/document filesystem workflow.

See [docs/roadmap.md](docs/roadmap.md) for phases and stop lines.

---

## Stack (planned)

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
   Native shell + UI        Extraction
```

| Layer | Choice | Owns |
| --- | --- | --- |
| Desktop shell | Tauri v2 + Rust | App state, filesystem, documents, future SQLite, search, jobs, calls to AI |
| UI | React + TypeScript + Vite | Editor, panels, interactions, visualizations |
| Editor (later) | CodeMirror 6 | Markdown editing |
| AI service | FastAPI + Pydantic + uv | LLM, research agents, extraction, fact check (stubs first) |
| Target OS | Linux first | `cargo tauri dev` now; AppImage later |

Rust owns the application. Python provides intelligence. They talk over local HTTP + OpenAPI — not shared memory, not one mega-process.

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

Until then, read the docs and follow [docs/todo/phase-1-writer.md](docs/todo/phase-1-writer.md).

---

## Documentation map

| Doc | What it is |
| --- | --- |
| [docs/architecture.md](docs/architecture.md) | Why Rust vs Python, filesystem, future SQLite, boundaries |
| [docs/domain-model.md](docs/domain-model.md) | Idea, Claim, Source, Evidence, Document, Relationship |
| [docs/roadmap.md](docs/roadmap.md) | Phases 1–5 with stop lines |
| [docs/todo/](docs/todo/) | Ordered tasks per phase (you-own / co-implement / guide-only) |
| [docs/monorepo.md](docs/monorepo.md) | Two languages in one repo without pain |
| [docs/learning-path.md](docs/learning-path.md) | What to learn before each phase |
| [docs/working-agreement.md](docs/working-agreement.md) | How guide + co-implement works on this project |

---

## License

TBD. For a public GitHub repo, **MIT** is the simple default when you are ready to add one.

---

## Commits

Prefer short conventional prefixes: `docs:`, `chore:`, `feat:`, `fix:`, plus one line of *why*. Use a longer body when the change needs explanation.
