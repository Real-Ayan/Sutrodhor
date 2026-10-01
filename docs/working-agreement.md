# Working agreement

How this project is built with a **full-project guide** and a **co-implementor** for boring or confusing parts.

---

## Roles

### You (product owner)

- Own direction, taste, and the GitHub story.
- Write **most** feature and domain code.
- Make **all** commits (unless you explicitly ask otherwise in a session).
- Decide when a phase stop line has been crossed.

### Guide + co-implementor (Cursor)

- Guide the **whole** project: architecture, sequencing, reviews, “what next,” learning path.
- **Co-implement** boring work (scaffolds, wiring, lint config, stub routes, FS boilerplate) and confusing work (Rust ownership, Tauri commands, error boundaries, HTTP contract).
- Draft code you can read, adjust, and commit — not a silent takeover of the product.

Default split: **you build the interesting product logic; we share the dull and the hard glue** so tooling does not eat six months.

---

## Task tags (used in `docs/todo/`)

| Tag | Meaning |
| --- | --- |
| **you-own** | You should drive design and first implementation |
| **co-implement** | Ask the guide early; pair or accept a draft for glue/confusion |
| **guide-only** | Discuss and decide; little or no code in that step |

---

## Good reasons to ask for co-implementation

- First Tauri app / first `#[tauri::command]`
- Project directory create/open helpers and error types
- FastAPI app skeleton, routers, Pydantic models, `/health`
- OpenAPI → Rust client glue
- ESLint/Prettier/ruff/clippy wiring
- “It works in my head but the borrow checker is winning”
- Stuck > ~30 minutes on environment or build issues

## Good reasons to keep you-own

- How claims and evidence should feel in the UI
- Domain rules and naming in the research graph
- Editor layout and writing workflow choices
- README voice and product framing
- What “good enough” means for a phase stop line

---

## What we will not do

- Generate the entire Sutrodhor product in one pass
- Ship fake AI that pretends to research or fact-check
- Fill the repo with dense “AI tutor” comments that advertise the tooling
- Add infrastructure fads before Phase 1 Writer works on Linux
- Replace your commits with a parallel ghost history

---

## Session habits that work

1. Point at a specific item in [todo/](todo/) or [roadmap.md](roadmap.md).
2. Say whether you want **guide** (explain/review), **co-implement** (write glue with you), or **review only**.
3. You commit with `docs:` / `chore:` / `feat:` / `fix:` and a clear why-line.
4. Stop at the phase stop line unless you consciously open the next phase.

---

## Commits and voice

- Conventional short prefixes; longer bodies when the change needs a story.
- Code should look like a careful human project on GitHub.
- Prefer teaching in `docs/` over novel-length inline comments.

---

## License note

No license file in the docs pass. Before the repo is public with real code, add one — **MIT** is the usual simple choice unless you have a reason for Apache-2.0.
