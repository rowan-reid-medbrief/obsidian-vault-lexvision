---
tags: [mri-133, medbrief, poc, split-detection, degraded-corpus, visual-guard]
repos: [claude_code/projects/annotations]
model_check: not-needed
parent: 2026-07-02-mri133-split-detection-geometric.md
---

# 2026-07-03 - MRI-133: last two SPLIT frontiers closed (degraded fixture + blank-page guard)

Closed the two SPLIT gaps the prior session flagged, taking the real corpus to ZERO silent errors on both populations. (1) A geometric seam-selector (`split_geometry.tiling_chains`) cracked the near-identical *template* case (bench): the true children partition the parent (their crop bands tile top-to-bottom, abutting at the seam) while look-alikes each fit a full overlapping crop - the neighbour-consistency signal was latent in the crop geometry already computed, so it was a selection-policy change, not the new sequence engine the handoff imagined (real clean SPLIT P66.7/R66.7/silent33 -> P100/R66.7/silent0/queue33). (2) Fixed the degraded OCR-collapse fixture bug (`scanning.degrade_file` dumped the OCR layer at one point) so degraded splits are matchable (real degraded SPLIT R0/silent66.7 -> R66.7/silent33; synthetic degraded SPLIT silent 100% -> 0%). (3) A lightweight visual safety guard (`split_visual.py`) flags the blank-page case (gp) for review instead of silently dropping it - the pure-white second child is unplaceable by any page-local signal, so it is queued, not resolved (a feasibility render settled that scope before any build).

269 tests pass (10 new). Committed to main: `72b40a5` (degraded fix + visual guard) and `d607ad8` (backlog groom), on top of the session's earlier seam-selector `a0c7ae0`; `feat/split-containment-detection` merged and deleted. Main has 4 unpushed commits and NO git remote configured (and no gh CLI), so pushing needs a remote set up first - deferred, and the top of the continuation. Backlog groomed: pagination fuse `[parked]`, the 6 completed split items normalised to `[done]`/`[routed-out]`, and the live next is the `[high]` bipartite coverage-graph reframe. Full arc: `docs/DESIGN-NOTES.md` 2026-07-03, `docs/plans/before-numbers/BASELINE.md`.

## Continuation Prompt

## Continuation: MRI-133 bipartite coverage-graph reframe (the architectural home for the cardinality logic)

**Parent session:** 2026-07-03-mri133-split-frontiers-degraded-and-blank.md

### Context
MRI-133 PoC (medbrief), `~/claude_code/projects/annotations`. Cardinality-aware page reconciliation so annotations/redactions transfer correctly when a records bundle is re-sorted. SPLIT detection is now fully handled (resolve-or-safe-queue, zero silent errors on the real corpus, both populations). The next build is the structural reframe the whole approach has been converging on.

### What was done (this session + recent)
- **SPLIT solved end to end**: token-space containment pipeline -> geometric seam-selector (cracked near-identical *template* pages via band-tiling geometry already computed) -> degraded OCR-collapse fixture fix -> blank-page visual safety guard. Zero silent SPLIT errors on the real corpus, both populations. 269 tests.
- **Backlog groomed**: pagination fuse `[parked]`; the coverage-graph reframe is the live `[high]`; 6 completed split items normalised to `[done]`/`[routed-out]`.

### Current state
- `main`: 4 unpushed commits (`513e853`, `a0c7ae0`, `72b40a5`, `d607ad8`). **No git remote configured, no `gh` CLI.**
- Working tree clean. `feat/split-containment-detection` deleted (merged). Real docs under `poc/data/real-*` (git-ignored).

### Where we left off
Everything committed locally; SPLIT is done and validated. Ready to start the coverage-graph reframe (a real architectural change - plan before building).

### Next steps (priority order)
1. **[do first - loose end] Push `main`.** 4 unpushed commits, no remote and no `gh` CLI here. Set up a private remote and push. Deferred this session pending a destination you control.
2. **[high] Implement the bipartite coverage-graph reframe** (`docs/IDEAS.md`). Replace one-to-one Hungarian + per-row split/clone/removed exceptions with a capacitated coverage graph; read the outcome off node degree (out-deg 1 + full = MATCHED; >=2 partial tiling = SPLIT; >=2 full = CLONE; 0 = REMOVED; mutated in-deg 0 = INSERTED). Min-cost-flow / ILP family. This is the home for the split logic + geometric subsystem. **Plan it first** (Opus/high; offer `/harden-plan`) - it touches the assignment backbone and decision policy.
3. `[med]` Coverage-floor / margin fallback for REMOVED on un-paginated docs.
4. `[med]` Anchor-partition + affine-gap alignment stage (brings page *order* into the model).
- `[parked]` Pagination-channel fuse into the content arm (revisit after the reframe).

### Key references
- `docs/IDEAS.md` (coverage-graph item), `docs/DESIGN-NOTES.md` (2026-07-02 + 07-03), `docs/plans/before-numbers/BASELINE.md`, `research/Cardinality-Aware Reconciliation ...pdf`.
- Source: `matchers/{decision,split_geometry,split_visual,base,assignment}.py`, `config.py`.
- Tests: `poc/.venv/bin/python -m pytest -q` (from `poc/`). Real bake-off: `poc/.venv/bin/python scripts/real_bakeoff.py --population both --by-case`.

### Notes for next session
- Suggested setup: **Opus / high** (architecture). The reframe touches the assignment backbone and decision policy; plan it (consider `/harden-plan`) before building.
- The reframe must **preserve** the current behaviour (zero silent SPLIT, resolve-or-queue) while unifying the four cardinality cases under one model.
- No reflection findings were deferred to IDEAS this session (the one `/whats-next` finding is a terminal observe learning).
