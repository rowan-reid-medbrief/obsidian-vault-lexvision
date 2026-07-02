---
date: 2026-07-02
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Real-data matcher bake-off, stamp-survival spike (NO-GO), pagination matcher, degraded population
type: wrap-up
tags: [mri-133, annotations, medbrief, matcher, bake-off, pagination, stamp-survival, real-data, docsorter, split-detection]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 049371e
model_check: fired-upgrade (model; Sonnet->Opus for the shared content_fraction/matcher fix)
---

## Session Summary

Ran the MRI-133 matcher bake-off on real (Azure-sourced) case documents, which surfaced and fixed three harness bugs (discarded Hungarian assignment, boilerplate counted as content, a false-SPLIT storm plus non-genuine synthetic splits), taking the real-data content-arm ensemble from POOR to GOOD. Answered the top-ranked open spike with a NO-GO: a durable page-dictionary id does NOT survive MedBrief's real `PagePushBack` merge (not just the already-known flatten path), so the durable id should be the DB `Page.id` on the never-merged `Page.pdfFile`, not an in-PDF stamp. Built a pagination-sequence matcher (reads printed "Page X of Y"; closes the safety-critical REMOVED silence and resolves CLONE, but not split - the footer marker travels to only one child) and wired a `--population clean|degraded|both` axis into the bake-off (the content arm collapses on scanned pages while `stamped_id` holds), confirming SPLIT is unsolved by every channel. All work merged to main (linear history, incl. the prior session's population-correction commit that had not reached main); a commissioned deep-research report on cardinality-aware reconciliation was filed to `docs/research/`, and a drafted handoff prompt points the next session to read it first.
