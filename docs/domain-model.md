# Domain model

Conceptual model for Sutrodhor. Implement only what the current phase needs; keep these names stable so the graph can grow without renaming everything later.

---

## Why this model exists

A draft is prose. Research is structure. Sutrodhor’s bet is that **claims and evidence should be first-class**, not buried forever inside a single Markdown file.

The document remains important — it is how the story is told — but it is fed by a small set of research objects.

---

## Core concepts

### Idea

A seed: a question, angle, hypothesis, or narrative direction. Soft and early. Ideas can spawn claims or outlines later.

Examples: “Explain how municipal budgets fail transparency” · “Episode on river pollution and paper mills”.

### Claim

A statement that can be supported, partially supported, contradicted, or left unverified.

Examples: “Plant X discharged Y tons of effluent in 2019” · “Voters distrust local budget dashboards”.

Claims are the spine of nonfiction and investigative work.

### Source

Something you drew from: URL, PDF, interview notes, book, dataset, Markdown clip.

A source has metadata (title, author, date, locator) and raw or extracted content. Sources are not claims; they are where claims might be grounded.

### Evidence

A specific span or fact drawn from a source that speaks to a claim: a quotation, figure, paraphrase with locator.

Evidence links **Claim ↔ Source**. One source can support many claims; one claim can rest on many evidence items.

### Document

A Markdown (or later rich) writing surface in the project: script, notes, outline, draft.

Documents **use** research; they are not the research database. Early phases treat documents as filesystem Markdown with UUID identity.

### Relationship

An explicit edge between objects: claim supported by evidence, evidence extracted from source, idea motivates claim, document cites claim, etc.

Relationships are what turn a pile of notes into a graph you can reason about (and eventually fact-check).

---

## Conceptual graph

```text
Idea
 │
 ▼
Claim ──────► Source
 │              │
 ▼              ▼
Evidence ◄──────┘
 │
 ▼
Document
```

Read it as:

- Ideas motivate claims.
- Claims point at sources (and are tested against them).
- Evidence is the concrete bridge between claim and source.
- Documents narrate using claims/evidence (citations, outline nodes, later story structure).

---

## Identity

Planned typed IDs (Rust direction):

| ID | Identifies |
| --- | --- |
| `ProjectId` | A project on disk |
| `DocumentId` | A document (UUID; maps to a path under `documents/`) |
| `IdeaId` | An idea |
| `ClaimId` | A claim |
| `SourceId` | A source |
| `EvidenceId` | An evidence item |

**UUID + filesystem:** the UUID is stable for linking and UI state; the `.md` path is what humans and git see. Keep a mapping (in `project.toml` or a small manifest under `.sutrodhor/`) so renames do not break links forever.

Do not use loosely typed string maps as the long-term model. Prefer structs and enums when you code this.

---

## Claim support states (Phase 3 direction)

Not implemented yet — names to remember:

- supported
- partially_supported
- contradicted
- unverified

These states hang off claim–evidence (and maybe claim–source) relationships, not off vibes in the draft alone.

---

## What to implement when

| Phase | Domain work |
| --- | --- |
| 1 Writer | `Project`, `Document`, IDs, FS paths — enough to open/edit/save |
| 2 Researcher | `Source`, research notes, first evidence/claim extraction shapes |
| 3 Thinker | Relationships, support states, graph views |
| 4 Storyteller | Outline/story structures linking documents to claims |
| 5 Agents | Same model; agents read/write via app APIs, not private Python state |

Until Phase 2, the Context panel can literally say “Coming soon” for Research / Claims / Sources / Evidence.

---

## Naming freedom

If a term fights you in UI copy (e.g. “Idea” vs “Angle”), change labels — keep the underlying concepts. Prefer one vocabulary in code and docs so GitHub readers can follow the thread.
