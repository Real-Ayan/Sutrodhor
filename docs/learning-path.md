# Learning path

Mentor sequence: what to learn **just before** you need it. Skip pure-Rust UI frameworks (egui/iced) for now so the product moves.

Teaching lives here. Keep committed code comments calm and professional — not a tutorial transcript.

---

## Mindset

You are building a **product**, not a Rust course. Learn in thin slices:

1. Enough to implement the next checklist item in [todo/](todo/).
2. Note confusion; ask the guide / co-implementor for the glue.
3. Move on; deepen later when the domain demands it (SQLite, async jobs, streaming).

---

## Before any Phase 1 coding

**Goal:** create stubs and understand the desktop boundary.

| Topic | Why | Enough looks like |
| --- | --- | --- |
| Rust modules + `Result` | App core will return errors, not panic | You can read `fn foo() -> Result<T, E>` without fear |
| `serde` (concept) | `project.toml` and JSON over HTTP | Serialize a small struct to JSON once |
| Tauri commands | UI calls Rust | One command round-trip: button → Rust → string back |
| React + TypeScript basics | Three-pane layout | Components, props, simple state |
| Vite mental model | Dev server + build for the webview | `npm run dev` / `tauri dev` |

**Skip for now:** advanced lifetimes, unsafe, custom allocators, full async Rust runtime deep dive.

**Co-implement candidates:** first Tauri project scaffold, first command, lint/format configs.

---

## During Phase 1 (Writer)

| Topic | Why |
| --- | --- |
| Paths and FS in Rust | Create project dirs, read/write Markdown |
| UUID | `DocumentId` stable identity |
| Controlled state in React | Open tabs, dirty flags, autosave timers |
| CodeMirror 6 basics | Markdown editor surface |
| Simple command palette UX | Expandable command list |

**Practice project (optional):** a tiny CLI that creates `project.toml` + `documents/` — then fold that logic into Tauri commands.

---

## Before SQLite (late Phase 1 / Phase 2)

| Topic | Why |
| --- | --- |
| “Index vs source of truth” | [architecture.md](architecture.md) — FS wins for `.md` |
| `rusqlite` **or** `sqlx` at a glance | Pick one when you implement; don’t learn both deeply first |
| Migrations as plain SQL files | Keep schema changes boring |

**Still skip:** ORMs that hide SQL completely, distributed DB fantasies.

---

## Before Phase 2–3 research objects

| Topic | Why |
| --- | --- |
| Domain vocabulary | [domain-model.md](domain-model.md) |
| Modeling relationships | Edges as data, not only nested JSON blobs |
| Metadata for sources | Title, URL, retrieved-at, content hash |

Extraction quality can wait; **shapes** of Claim / Source / Evidence should not.

---

## Before wiring real AI (Phase 5, some hooks earlier)

| Topic | Why |
| --- | --- |
| HTTP from Rust | `reqwest` (or similar) to FastAPI |
| Pydantic models you already know | Shared contract with OpenAPI |
| Timeouts and process lifecycle | Start/stop AI server; fail soft in UI |
| Streaming (later) | SSE or streamed responses for writing assistance |

You already know FastAPI — lean on that. The new muscle is **Rust as the client** and **persisting results in the app**, not leaving gold in Python RAM.

**Typer:** optional CLI later; learn it when you want terminal workflows, not as the desktop boundary.

---

## What not to study yet

- Kubernetes, Redis, Kafka, vector databases as a prerequisite
- Building your own editor from `<canvas>`
- Pure Rust GUI to “be more native” (Tauri + web UI is native enough for this product)
- Training or hosting local LLMs as a blocker to Phase 1

---

## How to use the guide

When a [todo](todo/) item is tagged **co-implement**, bring it to the guide early. When it is **you-own**, try a first pass; ask for review, not a rewrite of your whole design.

When stuck more than ~30 minutes on tooling, stop grinding — that is exactly what co-implement is for.
