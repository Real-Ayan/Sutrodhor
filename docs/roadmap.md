# Roadmap

Staged product roadmap. Checkboxes are intentional: unchecked means **not done**, not “pretend it exists.”

**Current focus:** documentation complete → next: empty app stubs → FastAPI `GET /health` → desktop shell → project/document FS workflow.

Detailed task lists live in [todo/](todo/).

---

## Phase 1 — Writer

Native writing shell. No research graph yet.

- [ ] Native application shell (Tauri + React, Linux)
- [ ] Project creation/opening
- [ ] File tree
- [ ] Markdown editor (CodeMirror 6)
- [ ] Multiple documents/tabs
- [ ] Save/autosave
- [ ] Basic search
- [ ] Command palette
- [ ] Keyboard shortcuts

**Stop line:** You can create a project, edit Markdown in tabs with autosave, reopen the project, and see placeholder Context sections. Do not start claim extraction or LLM calls here.

→ Tasks: [todo/phase-1-writer.md](todo/phase-1-writer.md)

---

## Phase 2 — Researcher

Bring sources into the project. Still mostly structured notes, not a full argument map.

- [ ] Add source
- [ ] URL import
- [ ] Markdown/text source
- [ ] PDF source
- [ ] Source metadata
- [ ] Research notes
- [ ] Claim extraction
- [ ] Evidence objects

**Stop line:** Sources and evidence exist as real objects tied to the project; extraction may still be stubby or assisted. No full contradiction engine yet.

→ Tasks: [todo/phase-2-researcher.md](todo/phase-2-researcher.md)

---

## Phase 3 — Thinker

Relationships and epistemic status.

- [ ] Claim/source relationships
- [ ] Evidence relationships
- [ ] Supported / partially-supported / contradicted / unverified states
- [ ] Fact checking
- [ ] Argument map
- [ ] Research graph
- [ ] Contradiction detection

**Stop line:** You can see how claims stand relative to evidence. Story generation waits for Phase 4.

→ Tasks: [todo/phase-3-thinker.md](todo/phase-3-thinker.md)

---

## Phase 4 — Storyteller

From research structure into narrative artifacts.

- [ ] Outline generation
- [ ] Research → outline
- [ ] Outline → draft
- [ ] Story structure
- [ ] YouTube/nonfiction workflow
- [ ] Narrative graph

**Stop line:** Outlines and drafts are grounded in claims/evidence. Full autonomous agents wait for Phase 5.

→ Tasks: [todo/phase-4-storyteller.md](todo/phase-4-storyteller.md)

---

## Phase 5 — Agentic workflows

Intelligence as workflows, still with Rust owning state.

- [ ] Research agent
- [ ] Evidence gathering
- [ ] Claim verification
- [ ] Writing assistance
- [ ] Context-aware AI actions
- [ ] Background jobs
- [ ] Streaming AI responses

**Stop line:** Agents help; they do not become a second source of truth. Optional Typer CLI can wrap the same Python capabilities for terminal use.

→ Tasks: [todo/phase-5-agents.md](todo/phase-5-agents.md)

---

## Explicit non-goals (for a long time)

Do not drag these in “just in case”:

- Kubernetes, Redis, Kafka
- Hosted multiplayer collaboration
- Auth/cloud accounts as a blocker to local writing
- Local LLM infra as a Phase 1 requirement
- Rewriting the UI in pure Rust (egui/iced) unless you choose that later on purpose

---

## Suggested build order after docs

```text
Docs (this) → empty crates/packages → FastAPI /health
  → Tauri three-pane shell → project + Markdown FS
  → CodeMirror + tabs + autosave → command palette stub
```

See [learning-path.md](learning-path.md) for what to study before each jump, and [working-agreement.md](working-agreement.md) for guide vs co-implement vs you-own.
