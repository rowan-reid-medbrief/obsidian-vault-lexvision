---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Safe-queued the exact-duplicate twin split (MRI-133 silent error #3) - the last real silent SPLIT retired
type: wrap-up
tags: [mri-133, annotations, matchers, split, coverage-graph, content-arm, medbrief]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 95f0e265e37ac73d84c11fbf6d74e6eb8a2b8fa0
parent: 2026-07-03-mri133-in-matcher-ocr-image-only.md
model_check: not-needed
---

## Session Summary

Retired the last real silent SPLIT error (bench-115132's exact-duplicate twin) by proving it information-theoretically unresolvable on page-local content - the split page and its surviving duplicate are byte-identical in text AND geometry - and shipping a monotone-safe safe-queue rule (`twin_split_abstain`, default on) that flags it for review instead of guessing, after measuring that the naive "let the split compete" approach merely relocated the error. 300 tests pass; committed + pushed `95f0e26`. The aggregate bake-off re-read (confirmatory only) kept getting killed on OCR and is carried into the handoff.
