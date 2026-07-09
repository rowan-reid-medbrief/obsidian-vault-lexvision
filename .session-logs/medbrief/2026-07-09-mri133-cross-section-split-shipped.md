---
tags: [mri-133, medbrief, annotations, matchers, split-resolution, coverage-graph, safety-gate, ship]
repos:
  - annotations: 063e22e
model_check: not-needed
---

# 2026-07-09 - MRI-133: cross-section (scatter) split resolution shipped

Built and shipped the cross-section (scatter) split resolver for MRI-133 per the hardened plan: an upgrade-only rescue in `coverage_graph._classify` (fires only on a base AMBIGUOUS/REMOVED, so it never regresses a confident page) gated by a 6-part decisiveness test (band-order tiling, union coverage, per-band uniqueness as the adjacency replacement, a single decisive chain, a two-axis x-spread guard, twin safety), plus `band_order_chains` (a shared `_chain_walk`), 8 unit fixtures, and the `cross_section` gate scenario (kept out of CATALOGUE). The ship gate PASSED at cap-120 (`scripts/rescue_safety_gate.py`, which collapsed the lever_a/median_rescue near-copies): zero new SILENT_ERROR ids on both ref types, 2 real scatters resolved at scatter-upgrade precision 1.0, the boilerplate-heavy rest safely abstained (a safe partial win; content-arm DoD still MARGINAL). Committed `063e22e`; full suite 344 green with the dial default ON; output-neutrality byte-identical. Also closed the logged `--skip-degrade` perf item.

Loose end for next time: the `mri133-annotations-poc` programme spine is 16+ days stale (last_synced 2026-06-23, still reads "M2 done, demo-ready") - the coverage-graph reframe, in-matcher OCR, split-vs-twin, render caching, the fusion hybrid, and today's cross-section ship all landed since and are not reflected. Re-sync it before the next `/programme next`. Content-arm levers are now largely exhausted; the honest remaining story to Deon is stamp-at-extraction for the content-unresolvable residual (c/d milestones stay blocked on Deon).

Process note: piping a long-running background command through `tail -N` hides all interim output until EOF (tail without -f only flushes at EOF) - use `python -u` + a raw redirect, or `tail -f`, to watch a ~75-min gate live.
