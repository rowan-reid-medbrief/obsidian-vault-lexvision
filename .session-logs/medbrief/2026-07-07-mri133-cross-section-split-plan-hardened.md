---
type: handoff
tags: [mri-133, annotations, content-arm, matcher, split, harden-plan, whats-next, medbrief]
repos:
  - annotations: 8d824ba
parent: 2026-07-05-mri133-median-rescue-hybrid-shipped.md
model_check: switched sonnet -> opus/xhigh for the plan + harden work
---

# MRI-133: cross-section split plan drafted and hardened

Groomed the annotations backlog (/whats-next), then drafted and hardened (/harden-plan, 8 critics + pre-mortem) the plan for the paired `[high]` cross-section (scatter) split-resolution items. The hardening refuted the draft's core premise (page-local geometry is not "strictly stronger" than mutated-index adjacency on assembled/boilerplate pages), and Rowan chose to build it properly: an upgrade-only rescue plus a per-band decisiveness gate that replaces the global consistency adjacency was cheaply providing. Plan committed (`8d824ba`); no code built yet (Phase 1 is fixtures-first).

## Continuation Prompt

## Continuation: MRI-133 cross-section (scatter) split resolver - build Phase 1

**Parent session:** 2026-07-07-mri133-cross-section-split-plan-hardened.md

### Context
MRI-133 content arm (annotations repo, branch `feat/coverage-graph-reframe`). Two paired `[high]`
backlog items: confidently resolve a page split whose children land in *different clinical sections*
of a re-sorted bundle (currently safe-queued, not resolved), plus its test fixture. The plan is
drafted and hardened; this session builds it.

### What was done this session
- Groomed the backlog (/whats-next): tagged the dormant REMOVED coverage-floor rule `[low]`; closed
  the corpus-expansion status checkpoint.
- Drafted `plans/2026-07-05-cross-section-split-plan.md`, then hardened it (/harden-plan, 8 critics +
  pre-mortem). Hardening refuted the draft premise; Rowan chose "build with a decisiveness gate".
- Logged one reflected learning to `docs/IDEAS.md` (adjacency = a cheap global-consistency guard).
- Committed: `8d824ba` (plan + backlog), vault `8d18d6f` (session hygiene).

### Current state
- Committed on `feat/coverage-graph-reframe`, local only (not pushed). No code built yet.
- The hardened plan is the spec of record. Design shape: an upgrade-only scatter rescue inside
  `coverage_graph._classify` (fires only when the non-scatter outcome is AMBIGUOUS/REMOVED), a
  `band_order_chains` geometry sibling, and a per-band decisiveness gate (uniqueness + single-chain +
  two-axis) that replaces adjacency's global consistency. Dial `split_cross_section_enable`, pinned OFF
  in `_NEUTRAL_CFG`. Ship gate: adversarial fixture passes AND zero-new-silent (both ref types, full
  stack, re-snapshot the median-rescue baseline) AND non-inert.

### Where we left off
Plan approved and committed. Offered to start Phase 1; Rowan ran /close-out then /handoff instead. No
implementation started.

### Next steps
1. **Phase 1 (fixtures-first, red-before-green):** write `poc/tests/test_split_cross_section.py` - case
   1 (MUST-RESOLVE) as the one red-first test, plus the MUST-ABSTAIN guards (adversarial
   assembled-from-repeated-blocks, ambiguous-reconstruction, image-only degenerate-x) green-today, and
   the plain-not-preempted + adjacent-unchanged anchors. Add the `cross_section` gate `Scenario`
   (split + scattering reorder) and confirm `test_mutate_oracle_faithful` still passes.
2. **Phase 2:** `_chain_walk` extraction + `band_order_chains` in `split_geometry.py`; the
   `split_cross_section_enable` dial; `_classify_base`/`_classify` split + `_cross_section_split` helper
   with the 6-part decisiveness gate. Flip the dial on in the fixture.
3. **Phase 3:** parameterise one `scripts/rescue_safety_gate.py`; run the full-stack gate (both ref
   types); re-run the median-rescue gate under the new `_classify`; confirm the golden fixture stays
   byte-identical (dial off); decide the default; write up in `DESIGN-NOTES.md`; close both backlog items.

Still-open alternative (unblocked, either-or, from the prior session): recalibrate tau_accept/tau_margin
for median's distribution, or report DoD MARGINAL as the honest content-arm ceiling to Deon.

Deferred this session to IDEAS: adjacency-as-global-consistency finding (under ## 2026-07-07 in
`docs/IDEAS.md`, `[low]`); run `/whats-next` to rank.

### Key references
- Plan: `plans/2026-07-05-cross-section-split-plan.md` (the spec of record).
- Touch points: `poc/src/mri133/matchers/coverage_graph.py` (`_classify`, split branch 183-232),
  `matchers/split_geometry.py` (`tiling_chains`/`_tiles_below`), `config.py` (dials + `_NEUTRAL_CFG` at
  test_output_neutrality.py:52), `matchers/ensemble.py` (`_apply_rescue`, the median-rescue composition),
  `scripts/median_rescue_safety_gate.py` (gate precedent to parameterise).
- Memory: `mri133-cardinality-channels` (updated with the corrected cross-section direction).

### Notes for next session
Model: this is safety-critical matcher work on Opus/xhigh; keep that tier for the build. The decisiveness
gate may abstain on most real scattered splits - a clean gate with a low upgrade count is a safe partial
win, not GOOD; the plan says to report it as such, and the fallback if it can't pass the adversarial case
is to close item #1 as a measured NO-GO routed to the sequence layer / stamp.
