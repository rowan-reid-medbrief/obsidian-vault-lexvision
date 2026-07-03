---
tags: [mri-133, medbrief, poc, split-detection, degraded-corpus, visual-guard]
repos: [claude_code/projects/annotations]
model_check: not-needed
parent: 2026-07-02-mri133-split-detection-geometric.md
---

# 2026-07-03 - MRI-133: last two SPLIT frontiers closed (degraded fixture + blank-page guard)

Closed the two SPLIT gaps the prior session flagged, taking the real corpus to ZERO silent errors on both populations. (1) A geometric seam-selector (`split_geometry.tiling_chains`) cracked the near-identical *template* case (bench): the true children partition the parent (their crop bands tile top-to-bottom, abutting at the seam) while look-alikes each fit a full overlapping crop - the neighbour-consistency signal was latent in the crop geometry already computed, so it was a selection-policy change, not the new sequence engine the handoff imagined (real clean SPLIT P66.7/R66.7/silent33 -> P100/R66.7/silent0/queue33). (2) Fixed the degraded OCR-collapse fixture bug (`scanning.degrade_file` dumped the OCR layer at one point) so degraded splits are matchable (real degraded SPLIT R0/silent66.7 -> R66.7/silent33; synthetic degraded SPLIT silent 100% -> 0%). (3) A lightweight visual safety guard (`split_visual.py`) flags the blank-page case (gp) for review instead of silently dropping it - the pure-white second child is unplaceable by any page-local signal, so it is queued, not resolved (a feasibility render settled that scope before any build).

269 tests pass (10 new). Committed to main: `72b40a5` (degraded fix + visual guard) and `d607ad8` (backlog groom), on top of the session's earlier seam-selector `a0c7ae0`; `feat/split-containment-detection` merged and deleted. Main has 4 unpushed commits and NO git remote configured (and no gh CLI), so pushing needs a remote set up first - deferred, and the top of the continuation. Backlog groomed: pagination fuse `[parked]`, the 6 completed split items normalised to `[done]`/`[routed-out]`, and the live next is the `[high]` bipartite coverage-graph reframe. Full arc: `docs/DESIGN-NOTES.md` 2026-07-03, `docs/plans/before-numbers/BASELINE.md`.
