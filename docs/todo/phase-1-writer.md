# Phase 1 — Writer (todo)

Ordered checklist. Tags: **you-own** · **co-implement** · **guide-only**

Parent roadmap: [../roadmap.md](../roadmap.md)

**Stop line:** Project create/open, Markdown tabs + autosave, reopen works, placeholder Context panel, command palette stub. No LLM, no claim graph.

---

## 0. Repo hygiene

- [ ] **you-own** — `git init` at repo root; first commit(s) for docs
- [ ] **co-implement** — Confirm `.gitignore` covers Rust/Node/Python/Linux artifacts
- [ ] **guide-only** — Agree commit message style (`docs:`, `chore:`, `feat:`, `fix:`)

---

## 1. Empty stubs + AI health

- [ ] **co-implement** — Create `apps/ai-server` with uv + FastAPI + Pydantic layout
- [ ] **co-implement** — `GET /health` returns a simple JSON ok payload
- [ ] **you-own** — Run health locally; note the command in README “How to run”
- [ ] **co-implement** — Placeholder routers/schemas for `/chat`, `/research`, `/extract-claims`, `/factcheck` (stub responses only)
- [ ] **co-implement** — Create `apps/desktop` Tauri v2 + React + TS + Vite skeleton (Linux)
- [ ] **co-implement** — Wire `rustfmt`/`clippy`, ESLint/Prettier, `ruff` lightly

---

## 2. Application shell (three panes)

- [ ] **you-own** — Sketch layout: Project tree | Editor | Context
- [ ] **co-implement** — Implement basic CSS/layout shell in React (no card farm; writing-first)
- [ ] **you-own** — Top bar: product name + menu/command entry point
- [ ] **you-own** — Context panel static sections: Research, Claims, Sources, Evidence (“Coming soon”)

---

## 3. Project filesystem

- [ ] **guide-only** — Confirm `project.toml` fields for v1 (name, id, document map)
- [ ] **co-implement** — Rust: create project dir (`project.toml`, `documents/`, empty `.sutrodhor/`)
- [ ] **co-implement** — Rust: open project (validate layout, load document list)
- [ ] **co-implement** — Native folder dialogs (or simple path form) via Tauri
- [ ] **you-own** — UI flows for Create Project / Open Project

---

## 4. Documents

- [ ] **co-implement** — Rust domain stubs: `ProjectId`, `DocumentId` (UUID), `Document` metadata
- [ ] **co-implement** — Create / read / write Markdown on disk
- [ ] **you-own** — File tree UI listing `documents/`
- [ ] **you-own** — Open document into editor area
- [ ] **co-implement** — CodeMirror 6 Markdown editor integration
- [ ] **you-own** — Tabs for multiple open documents
- [ ] **co-implement** — Autosave strategy (debounce + explicit save command)
- [ ] **you-own** — Verify: quit, reopen project, documents still there

---

## 5. Commands and shortcuts

- [ ] **you-own** — Command list design (open palette, new doc, save, toggle panels)
- [ ] **co-implement** — Basic command palette UI stub (expandable later)
- [ ] **you-own** — Keyboard shortcuts for the few commands that matter daily

---

## 6. Search (basic)

- [ ] **you-own** — Define “basic search” for v1 (filename vs in-file)
- [ ] **co-implement** — Minimal in-project text search over Markdown (no SQLite required yet)

---

## 7. Phase 1 exit checklist

- [ ] Desktop runs on Linux via `cargo tauri dev` / npm script
- [ ] Create + open project works
- [ ] Create/edit/save Markdown; tabs + autosave
- [ ] Reopen project shows documents
- [ ] Context placeholders visible
- [ ] AI `/health` works in sibling app
- [ ] README run instructions updated
- [ ] **guide-only** — Review stop line; explicitly open Phase 2 when ready

---

## Parked (not Phase 1)

SQLite schema, sources, claims, LLM calls, AppImage packaging, Docker, Typer CLI, pure-Rust UI rewrite.
