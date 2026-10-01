# Phase 5 — Agentic workflows (todo)

Ordered checklist. Tags: **you-own** · **co-implement** · **guide-only**

Requires a solid Writer + enough research/think/story structure that agents have something real to operate on.

Parent roadmap: [../roadmap.md](../roadmap.md)

**Stop line:** Agents assist via Rust-owned jobs and persisted results. Python never becomes the database of record.

---

## 1. Job system in the app

- [ ] **co-implement** — Background job model in Rust (queue, status, cancellation)
- [ ] **you-own** — UI: job list / progress / errors
- [ ] **co-implement** — Stream or poll AI responses into the UI honestly

---

## 2. Agents (capabilities, not a swarm for its own sake)

- [ ] **you-own** — Define agent actions: research, gather evidence, verify claim, writing assist
- [ ] **co-implement** — FastAPI agent modules + Pydantic I/O; stub → real models
- [ ] **co-implement** — Rust orchestration: call AI, validate, persist, notify UI
- [ ] **you-own** — Context-aware actions from selection / open claim / open doc

---

## 3. Writing assistance

- [ ] **you-own** — Commands that feel like a writing tool, not a chatbot dump
- [ ] **co-implement** — Streaming responses when it improves the UX
- [ ] **you-own** — Guardrails: show sources/claims used; allow undo

---

## 4. Optional CLI

- [ ] **co-implement** — Typer CLI wrapping the same Python services for terminal workflows
- [ ] **you-own** — Document when to use desktop vs CLI

---

## 5. Packaging (when the product deserves it)

- [ ] **co-implement** — Linux AppImage (or chosen packager)
- [ ] **guide-only** — Docker only if it helps AI/dev reproducibly — not required for desktop users

---

## 6. Phase 5 exit checklist

- [ ] At least one end-to-end agent action persists results into the project
- [ ] Jobs can fail without corrupting documents
- [ ] Streaming (if present) is cancellable
- [ ] Architecture boundaries still hold: Rust owns state; Python provides intelligence
- [ ] **guide-only** — Retire or rewrite roadmap for “beyond v1”

---

## Never-goals unless product direction changes

Multi-tenant cloud collaboration, plugin marketplace, rewriting the UI in egui “for purity,” or pretending agents replace editorial judgment.
