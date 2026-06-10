---
date: 2026-06-10
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: medbrief
session: Kumulus de-id annotation-tooling research and c3b DB-schema reconciliation across the dossier
type: wrap-up
tags: [kumulus, medbrief, lexvision, deep-research, de-identification, presidio, annotation-tooling, db-reconciliation, pii, ground-truth]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
  - path: /Users/Rowan.Reid/.claude
---

## Session Summary

Walked the Kumulus research in depth (the ten-module decomposition with per-module benchmarks, the canonical medico-legal entity model, and the per-module build methodology/technology/libraries), then answered Laura's ask on how clinicians could build the pseudonymisation ground truth with a deep-research-backed de-identification annotation-tool comparison (`research/c7-annotation-tooling.md`: Label Studio primary, INCEpTION runner-up, MedTator/Prodigy/Argilla situational, with the load-bearing South et al. 2014 caveat that a noisy machine pre-annotation pass can degrade quality, so tune Presidio for precision and pilot first; Presidio confirmed as the "simple AI" first pass Laura described). Closed by reconciling the attended `c3b` DB-schema capture into the living models (`c5` re-anchored on `matterrequestpatient` and `clinicalsummary`, `d1` build-split hinges #2 OCR and #3 PII-detector settled) and date-stamping the stale overnight snapshots (`09`, `OVERNIGHT-REVIEW`, stream1/2-evidence, `c3`, `d2`) with forward-pointers rather than rewriting history; ADR-005 left untouched (append-only, the four-entity-detector finding reinforces it). Open: send Stream 1 plus the c7 summary to Laura and Deon, chase the 5 named-person confirmations (Deon, NICE, Agilio), and decide whether to brand the Stream 2 companion.
