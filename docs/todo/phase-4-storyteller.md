# Phase 4 — Storyteller (todo)

Ordered checklist. Tags: **you-own** · **co-implement** · **guide-only**

Requires Phase 3 relationships and support states to be trustworthy enough to ground a story.

Parent roadmap: [../roadmap.md](../roadmap.md)

**Stop line:** Outlines and drafts can be grounded in research objects. Full agentic loops wait for Phase 5.

---

## 1. Outline as a first-class artifact

- [ ] **you-own** — Decide outline format (Markdown sections vs structured outline nodes)
- [ ] **co-implement** — Link outline nodes to claims/evidence IDs
- [ ] **you-own** — Editor/UX for outline ↔ draft navigation

---

## 2. Research → outline → draft

- [ ] **guide-only** — What the AI is allowed to invent vs must cite
- [ ] **co-implement** — Python endpoints for outline suggestions; Rust persists accepted results
- [ ] **you-own** — “Accept / edit / reject” flow — never silent overwrite of the draft
- [ ] **you-own** — Outline → draft expansion that preserves claim links

---

## 3. Story structure / nonfiction workflows

- [ ] **you-own** — YouTube/nonfiction template(s) as optional project types or presets
- [ ] **you-own** — Narrative graph: how story beats attach to research graph
- [ ] **co-implement** — Minimal data model for beats/scenes if needed beyond Markdown

---

## 4. Phase 4 exit checklist

- [ ] Can produce an outline from selected research with human approval
- [ ] Draft remains filesystem Markdown you control
- [ ] Citations/links to claims survive edits at a basic level
- [ ] **guide-only** — Stop line review before Phase 5

---

## Parked

Always-on agents, background multi-step research crews, streaming token UIs (those are Phase 5).
