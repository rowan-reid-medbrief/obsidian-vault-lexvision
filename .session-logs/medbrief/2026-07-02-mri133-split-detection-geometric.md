---
tags: [mri-133, medbrief, poc, split-detection, geometry, bakeoff]
repos: [claude_code/projects/annotations]
model_check: not-needed
parent: 2026-07-02-mri133-real-data-bakeoff-stamp-spike-pagination.md
---

# 2026-07-02 - MRI-133: SPLIT detection (containment -> set-cover -> adjacency + geometric substrate)

Built SPLIT detection end to end from the commissioned deep-research report, whose thesis is that splits are a *containment* problem, not a *resemblance* one (Broder). A token-space pipeline in `decision.py` (containment selection -> greedy weighted set-cover -> adjacency guard) took real clean SPLIT from 100% silent to 33% silent (50% recall / 60% precision): it confidently resolves a clean, adjacent, text-bearing split and safely queues the rest. A geometric substrate (`matchers/split_geometry.py`: RANSAC translation+scale crop fit over distinctive word boxes) filters look-alikes by transform residual and supplies the real source-region bands for annotation transfer; it holds the headline metric and generalises past the adjacency heuristic. Also reconstructed and committed the real-data bake-off harness (`scripts/real_bakeoff.py`) that was the decisive instrument (the synthetic corpus could not test the change: its clean population never triggers the resemblance gate and its degraded OCR layer is spatially collapsed).

The two remaining SPLIT gaps are proven to need capabilities beyond page-local evidence: near-identical *template* pages (all fit a crop of the parent, so neither token overlap nor crop residual separates the true children - needs sequence / neighbour-consistency context) and blank/near-blank pages (no text - needs the visual channel). Both logged in `docs/IDEAS.md`. 250 tests pass; two commits on branch `feat/split-containment-detection`, not merged to main. Full arc in `docs/DESIGN-NOTES.md` (three 2026-07-02 SPLIT entries) and `docs/plans/before-numbers/BASELINE.md`.
