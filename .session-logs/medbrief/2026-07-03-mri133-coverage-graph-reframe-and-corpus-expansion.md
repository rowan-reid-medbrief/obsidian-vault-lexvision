---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Coverage-graph reframe (output-neutral IR overlay) + first private GitHub remote + real corpus 3->11 docs; REMOVED margin rule built dormant
type: wrap-up
tags: [mri-133, medbrief, coverage-graph, harden-plan, matchers, corpus-expansion, github-remote]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 218f522
parent: 2026-07-03-mri133-split-frontiers-degraded-and-blank.md
model_check: not-needed
---

## Session Summary

Built the MRI-133 bipartite coverage-graph reframe as an output-neutral IR overlay (`matchers/coverage_graph.py` + `content_tokens.py`; `decide()` now a thin compat shim), planned and `/harden-plan`'d first, which correctly dropped the originally-planned capacitated-solver backbone (it could not be output-neutral, and the research report never wanted it as the backbone). Verified byte-identical via a committed 2160-prediction golden fixture, 290 tests, and the real bake-off (zero silent both populations, DoD GOOD, unchanged vs BASELINE.md); committed on `feat/coverage-graph-reframe` (218f522) and pushed to a newly-created private GitHub remote (`rowan-reid-medbrief/mri-133-annotations`, the repo's first). Also folded in the report's p7 REMOVED margin rule but shipped it DORMANT (dials default OFF), and expanded the real test corpus 3->11 docs from Azure across all four provenances (incl. two real image-only docs + a 1344pp trust doc), teeing up the next session's stamp+wire+measure build.
