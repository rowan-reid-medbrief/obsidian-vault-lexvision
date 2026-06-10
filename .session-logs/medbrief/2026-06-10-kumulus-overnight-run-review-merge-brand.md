---
type: session
date: 2026-06-10
project: lexvision-poc
domain: medbrief
tags: [kumulus, medbrief, lexvision-poc, overnight-run, deep-verification, db-schema, medbrief-brand]
repos:
  - lexvision-poc@b2d7227
  - ~/.claude@24e6316
  - ObsidianVault
parent: 2026-06-09-kumulus-dossier-lexvision-poc
---

# 2026-06-10 — Kumulus overnight run: executed, reviewed, corrected, merged and branded

Executed the unattended Kumulus research pipeline (`/overnight-run`) to completion (12 tasks verified and scoped-committed on `overnight/2026-06-09`; c3 degraded gracefully on the DB, d1 passed on a retry after a transient socket drop), then ran the attended morning review (`/overnight-plan review`). Captured the pre-staging `medbrief-live` schema attended (schema-only, via the jumpbox tunnel plus the expert-sheet venv; `c3b`, closing deep-verify #5) and worked all seven `d2` claims via a parallel read-only investigation (`d2b`): the "Kumulus already has entity-ID tooling" headline stays refuted, OCR reuse is Azure Document Intelligence, MedBrief's PII detector is a narrow four-entity rule-based redactor with no published recall, the NICE API is current-only, and training on NICE content is prohibited. Folded the corrections into the stream1 deliverable, fast-forward merged into `main`, prepped the slide-11/13 assets, and produced the MedBrief-branded `stream1-laura-asks.docx` (extending `medbrief-brand`'s docx builder with image and hyperlink support). Five residual confirmations remain for named people (Deon, NICE, Agilio), all recorded in `d2b`.
