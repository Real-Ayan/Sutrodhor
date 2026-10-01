# Monorepo guide

How two (really three) toolchains live in one Git repo without turning into a “platform.”

---

## Plain English

A **monorepo** here means: one Git repository, multiple apps, each with its own language tooling.

You do **not** need Turborepo, Nx, or a microservice mesh. You need:

- clear folders
- a README that says which directory to `cd` into
- maybe a root `Makefile` later for shortcuts

“Workspace” in npm/pnpm language means “multiple JS packages linked together.” Sutrodhor starts with **one** frontend app, so you can ignore JS workspaces until you actually split packages.

---

## Layout

```text
Sutrodhor/                    # repo root (capital S — keep it)
├── apps/
│   ├── desktop/              # Tauri v2 + React + TypeScript
│   │   ├── src/              # UI (React)
│   │   ├── src-tauri/        # Rust (app core)
│   │   └── package.json      # name: sutrodhor-desktop
│   └── ai-server/            # FastAPI
│       ├── app/
│       ├── pyproject.toml    # name: sutrodhor-ai, managed with uv
│       └── ...
├── docs/
├── README.md
└── .gitignore
```

Package and crate names: lowercase **`sutrodhor-*`**. Folder for the GitHub repo can stay **`Sutrodhor`**.

---

## Toolchain map

| Area | Tool | Where you run it |
| --- | --- | --- |
| Rust / Tauri | `cargo`, Tauri CLI | `apps/desktop/src-tauri`, via `npm run tauri` from `apps/desktop` |
| UI | Node + **npm** | `apps/desktop` |
| AI server | Python 3.12+ + **uv** | `apps/ai-server` |
| Format/lint (planned) | `rustfmt`/`clippy`, ESLint/Prettier, `ruff` | each app’s folder |

Why npm: one less concept while learning Tauri; switch to pnpm later if you care about disk and lockfile speed.

Why uv: fast, modern Python env + lockfile; you already have it.

---

## How to run each app (planned)

Apps are not created yet. When they are:

```bash
# Terminal A — AI service
cd apps/ai-server
uv sync
uv run uvicorn app.main:app --reload --port 8787

# Terminal B — desktop
cd apps/desktop
npm install
npm run tauri dev
```

Use a fixed local port for the AI server (e.g. `8787`) and put it in config once — do not scatter magic URLs.

Optional later:

```makefile
# root Makefile sketch
ai-health:
	cd apps/ai-server && uv run uvicorn app.main:app --port 8787

desktop:
	cd apps/desktop && npm run tauri dev
```

---

## The interface between Rust and Python

They do **not** share memory or import each other’s code.

Contract:

1. **Pydantic models** in `apps/ai-server/app/schemas/` define request/response shapes.
2. FastAPI exposes HTTP routes (`/health`, later `/chat`, `/research`, …).
3. OpenAPI is generated automatically — that is your interface document.
4. Rust calls `localhost` with an HTTP client; optionally generate types from OpenAPI later.

```text
React  --Tauri invoke-->  Rust  --HTTP JSON-->  FastAPI
                              <-- JSON --
```

UI should talk to Rust for anything that touches projects or files. UI calling Python directly is a shortcut that will hurt when you add jobs, permissions, and persistence.

### FastAPI vs Typer

| | FastAPI | Typer |
| --- | --- | --- |
| Role | Local HTTP service | CLI |
| Desktop integration | Natural | Awkward (subprocess + parse stdout) |
| When | Now (AI sibling app) | Optional later for terminal workflows |

Same business logic can back both eventually; start with FastAPI.

---

## What not to share

| Don’t put here | Put here instead |
| --- | --- |
| Open project path in Python globals | Rust app state |
| Authoritative Markdown only in AI responses | `documents/*.md` on disk |
| Secret API keys in the frontend bundle | OS keychain / env for the AI process (later) |
| One giant shared “utils” crate for UI strings | Keep UI copy in React |

Shared **ideas** (domain terms) live in docs and mirrored types — not a forced polyglot package on day one.

---

## Git and ignore rules

Ignore build artifacts for all three stacks (see root `.gitignore`). Commit:

- source
- lockfiles (`package-lock.json`, `uv.lock`, `Cargo.lock` for the app)
- docs

You own `git init` and commits. Suggested early commits are listed in the plan notes / README.

---

## Dependency discipline

Add a dependency only when a phase task requires it. Prefer:

- Tauri’s own APIs for dialogs/FS bridges
- std + small crates in Rust (`serde`, `uuid`, later `rusqlite` or `sqlx`)
- FastAPI + Pydantic + uvicorn in Python until real LLM work starts

If a README badge farm appears before `/health` works, something went wrong.
