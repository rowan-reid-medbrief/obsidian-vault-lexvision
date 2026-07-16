---
date: 2026-07-16
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: medbrief
session: Reviewed and documented Kumulus's Gen 4 "Data and AI PoV" proposal; logged ADR-009
type: wrap-up
tags: [kumulus, medbrief, lexvision-poc, proposal-review, ADR-009, patent-substantiation, pseudonymisation, compliance]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
    commit: PENDING
model_check: not-needed
---

## Session Summary

Moved Kumulus's latest proposal (the Gen 4 "Data and AI PoV" deck, received 9 July) into `source_material/kumulus/` and reviewed it against ADR-008's eight gating conditions and the 12 June regroup. The deck inverts scope back to the d1-recommended split: Kumulus now builds the upstream extraction pipeline (entity/attribute/relationship extraction, limited co-reference, pseudonymisation, graph-ready outputs, evaluation) and drops both OCR and the case-vs-guideline comparison layer, so MedBrief keeps the reasoning layer it wants to own. Documented the assessment as `docs/kumulus/12-review-2026-07-09-data-ai-pov.md` and ADR-009 (hold accept-in-principle-and-negotiate; five open items, the first a new compliance crux because pseudonymisation moving back to Kumulus means prepared case data with possible residual long-text PII now crosses to a Brazil-based vendor in Azure), and updated the dossier overview and project CLAUDE.md.
