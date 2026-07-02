---
tags: [mri-133, medbrief, poc, split-detection, geometry, bakeoff]
repos: [claude_code/projects/annotations]
model_check: not-needed
parent: 2026-07-02-mri133-real-data-bakeoff-stamp-spike-pagination.md
---

# 2026-07-02 - MRI-133: SPLIT detection (containment -> set-cover -> adjacency + geometric substrate)

Built SPLIT detection end to end from the commissioned deep-research report, whose thesis is that splits are a *containment* problem, not a *resemblance* one (Broder). A token-space pipeline in `decision.py` (containment selection -> greedy weighted set-cover -> adjacency guard) took real clean SPLIT from 100% silent to 33% silent (50% recall / 60% precision): it confidently resolves a clean, adjacent, text-bearing split and safely queues the rest. A geometric substrate (`matchers/split_geometry.py`: RANSAC translation+scale crop fit over distinctive word boxes) filters look-alikes by transform residual and supplies the real source-region bands for annotation transfer; it holds the headline metric and generalises past the adjacency heuristic. Also reconstructed and committed the real-data bake-off harness (`scripts/real_bakeoff.py`) that was the decisive instrument (the synthetic corpus could not test the change: its clean population never triggers the resemblance gate and its degraded OCR layer is spatially collapsed).

The two remaining SPLIT gaps are proven to need capabilities beyond page-local evidence: near-identical *template* pages (all fit a crop of the parent, so neither token overlap nor crop residual separates the true children - needs sequence / neighbour-consistency context) and blank/near-blank pages (no text - needs the visual channel). Both logged in `docs/IDEAS.md`. 250 tests pass; two commits on branch `feat/split-containment-detection`, not merged to main. Full arc in `docs/DESIGN-NOTES.md` (three 2026-07-02 SPLIT entries) and `docs/plans/before-numbers/BASELINE.md`.

## Continuation Prompt

## Continuation: MRI-133 SPLIT detection - sequence-context lever + open decisions

**Parent session:** 2026-07-02-mri133-split-detection-geometric.md

### Context
MRI-133 PoC (medbrief), `~/claude_code/projects/annotations`. We're building cardinality-aware page reconciliation so annotations/redactions transfer correctly when a records bundle is re-sorted. This session cracked SPLIT detection - the one case every prior channel failed on - acting on a commissioned deep-research report (splits are a *containment* problem, not *resemblance*).

### What was done this session
- Read the deep-research PDF in full; re-ranked `docs/IDEAS.md` and wrote a plan (`docs/plans/2026-07-02-split-unbind-resemblance-gate.md`).
- Built token-space SPLIT detection in `decision.py`: containment selection -> greedy weighted set-cover -> adjacency guard. Real clean SPLIT went **100% silent -> 33% silent, 50% recall / 60% precision**.
- Built the geometric substrate `matchers/split_geometry.py` (RANSAC translation+scale crop fit over distinctive word boxes): a residual filter that rejects look-alikes and supplies real source-region bands. Holds the metric, generalises past adjacency.
- Reconstructed + committed the real-data bake-off harness `poc/scripts/real_bakeoff.py` (the decisive instrument) and a diagnostic `poc/scripts/diagnose_real_split.py`.
- 250 tests pass. Two commits on branch `feat/split-containment-detection` (NOT merged to main).

### Current state
- Branch `feat/split-containment-detection`: `4a0d46d` (token-space) + `513e853` (geometry). **Not merged to main; main is local-only (unpushed).**
- Working tree clean. Real patient docs kept under `poc/data/real-*` (git-ignored).
- Full arc: `docs/DESIGN-NOTES.md` (three 2026-07-02 SPLIT entries), `docs/plans/before-numbers/BASELINE.md`.

### Where we left off
SPLIT is now partially solved: clean, adjacent, text-bearing splits resolve confidently with real source regions; everything else safely queues. Two cases remain unsolved by page-local evidence and are the next frontier.

### Next steps
1. **Decide the branch:** merge `feat/split-containment-detection` -> main (and whether to push main)? A your-call git decision I deliberately left open.
2. `[high]` **Sequence / neighbour-consistency lever** - the real next build. Near-identical *template* pages (bench case: 138-142 all fit a crop of 141) can't be resolved by page-local evidence; needs reading-order continuity across the seam, mutated-order adjacency, cross-boundary paragraph/table continuation. This would promote bench from safe-abstain to correct resolution.
3. `[high]` **Fuse the pagination channel into the content arm** - the parent handoff's deferred step, still open (`matchers/pagination.py`, not in the default REGISTRY).
4. `[med]` **Visual channel for blank-page splits** (gp case: 0 tokens, no text signal).
5. `[med]` **Fix the degraded-corpus OCR-collapse bug** (`scanning.degrade_file` dumps OCR text at one point, so degraded splits are degenerate - blocks degraded-population split testing).

### Key references
- `docs/IDEAS.md` (2026-07-02 block, re-ranked), `docs/DESIGN-NOTES.md`, `docs/plans/before-numbers/BASELINE.md`, the research PDF under `docs/research/`.
- Source: `matchers/decision.py`, `matchers/split_geometry.py`, `matchers/base.py`, `config.py`.
- Run the real bake-off: `poc/.venv/bin/python poc/scripts/real_bakeoff.py --population both --by-case`.

### Notes for next session
Suggested setup: Opus / high (architecture territory). The geometric metric didn't move the headline number on the 3-doc corpus (token-space already maxed the index-set metric there); its value is correct source regions + generalisation. Don't chase the headline SPLIT number with more token/geometry tuning - the remaining gaps need genuinely different signals (sequence context, vision).
