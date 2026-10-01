# Phase 3 — Thinker (todo)

Ordered checklist. Tags: **you-own** · **co-implement** · **guide-only**

Requires Phase 2 objects (sources, claims, evidence).

Parent roadmap: [../roadmap.md](../roadmap.md)

**Stop line:** Claim support states and relationships are visible; fact-check hooks exist. Storytelling waits for Phase 4.

---

## 1. Relationships

- [ ] **guide-only** — Enumerate relationship kinds needed first (claim–evidence, evidence–source, idea–claim, …)
- [ ] **co-implement** — Persist relationships (SQLite strongly recommended by now)
- [ ] **you-own** — UI to create/break links without editing raw DB

---

## 2. Support states

- [ ] **you-own** — Product rules for supported / partially_supported / contradicted / unverified
- [ ] **co-implement** — Encode states on claim–evidence (or claim aggregate)
- [ ] **you-own** — Show state clearly in Context and optionally in editor gutter/annotations

---

## 3. Fact checking

- [ ] **co-implement** — `POST /factcheck` contract (Pydantic) + Rust client
- [ ] **you-own** — UX: run fact-check on a claim; show result as data, not magic
- [ ] **you-own** — Keep human override — model output is advice

---

## 4. Graph views

- [ ] **you-own** — Argument map / research graph information design (keep simple)
- [ ] **co-implement** — Choose a visualization approach (e.g. modest graph lib) and wire data
- [ ] **you-own** — Contradiction detection: start with explicit opposing evidence, not ML theatre

---

## 5. Phase 3 exit checklist

- [ ] Relationships round-trip on disk/DB
- [ ] Support states visible and editable
- [ ] Fact-check path works end-to-end (even if model is weak)
- [ ] Graph view is useful for a small real project
- [ ] **guide-only** — Stop line review before Phase 4

---

## Parked

Full narrative generation, YouTube packaging workflow, autonomous multi-agent crews.
