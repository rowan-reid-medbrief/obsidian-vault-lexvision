---
date: 2026-06-18
project: /Users/Rowan.Reid/claude_code/medbrief-onboarding
domain: medbrief
session: MRI-133 research extended per Deon's follow-up and DB-verified against pre-staging; section 11 corrected
type: wrap-up
tags: [mri-133, medbrief, secure-review, database, annotations, docsorter, deon]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-onboarding
    commit: 5d48171bb76f0bb7a20cc51f2339a1a35ef8e908
parent: 2026-06-17-mri-133-research.md
model_check: not-needed
---

## Session Summary

Continued the MRI-133 research from Deon's reply, a green light plus an extension: what happens for documents that bypass DocSorter (client self-uploads, unsorted records). Using a read-only pre-staging DB connection, established that `Page` rows attach only to `BatchDocument`s, so every annotated document is page-less, and a direct check (1 of 5,536 annotated docs across the 30,564 `SortingSessionExportPusher` collections) put annotations on the raw records, not the re-ingested export bundle, so the drift MRI-133 describes does not bite current annotations. The investigation self-corrected several times (an Explore agent's confident "sorted output is just a ZIP" was incomplete; the data settled it); the landing point is data-confirmed and Rowan's Teams reply to Deon is accurate. This refutes the sibling `2026-06-18-mri-133-sorting-annotation-architecture` session's inference that annotations bind to the export bundle; that session's SALLi wiring and centre gating still stand.
