# Phase 2 — Researcher (todo)

Ordered checklist. Tags: **you-own** · **co-implement** · **guide-only**

Do not start until Phase 1 stop line is met.

Parent roadmap: [../roadmap.md](../roadmap.md)

**Stop line:** Sources and evidence exist as project objects; claim extraction can be assisted/stubbed. No full contradiction engine.

---

## 1. Source model

- [ ] **guide-only** — Agree source kinds for v1 (url, markdown/text, pdf)
- [ ] **you-own** — Define Source metadata fields (title, authors, retrieved_at, locator, …)
- [ ] **co-implement** — Rust types: `SourceId`, `Source`, persistence under `sources/` + metadata
- [ ] **you-own** — UI: add source / list sources in Context → Sources

---

## 2. Import paths

- [ ] **co-implement** — URL import: fetch bytes/text via Rust or delegated stub (honest errors)
- [ ] **you-own** — Paste / import Markdown or plain text as a source
- [ ] **co-implement** — PDF source: pick a simple library path; extract text later if needed
- [ ] **you-own** — Research notes linked to a source (Markdown under `research/` or similar)

---

## 3. Claims and evidence (shapes first)

- [ ] **you-own** — UX for creating a claim manually
- [ ] **co-implement** — Rust types: `ClaimId`, `EvidenceId`, storage layout
- [ ] **you-own** — Attach evidence (quote + locator) from a source to a claim
- [ ] **co-implement** — Placeholder Python `POST /extract-claims` wired from Rust (stub or heuristic only until real LLM)

---

## 4. Context panel becomes real

- [ ] **you-own** — Replace “Coming soon” with live lists for Sources / Claims / Evidence (Research can stay lighter)
- [ ] **co-implement** — Tauri commands to load context for open project
- [ ] **guide-only** — Decide how much still lives only on FS vs early SQLite index

---

## 5. Phase 2 exit checklist

- [ ] Add at least URL + text sources
- [ ] Manual claim + evidence works
- [ ] Extraction endpoint exists (stub ok if labeled)
- [ ] No fake “AI researched the web” theater
- [ ] **guide-only** — Review stop line before Phase 3

---

## Parked

Argument map UI, contradiction detection, streaming agents, narrative outline generation.
