---
name: mri133-cardinality-channels
description: "What each matcher channel can and cannot do on the hard cardinality cases (split/clone/removed/inserted). SPLIT is now FULLY HANDLED on the real corpus (zero silent errors, both populations): every text-bearing split resolves or safely queues, the degraded OCR-collapse fixture bug is fixed, and the one blank-page case is flagged for review not silently dropped. Pagination fuse still open."
metadata:
  type: project
  originSessionId: this-session
---

The MRI-133 matchers are one-to-one assignment machines; they break on **cardinality
changes** (a page becoming several, or none, or an inserted page). Measured reach (2026-07-03,
on the 3 real Azure docs and the synthetic corpus):

- **SPLIT is now FULLY HANDLED (was: unsolved by every channel, then partially).** Zero silent
  SPLIT errors on the real corpus, BOTH populations. The arc, all acting on the commissioned
  deep-research report (splits are a *containment* problem, not *resemblance* — Broder):
  1. **Token-space pipeline** in `decision.py` (containment selection → greedy weighted set-cover
     → adjacency guard) resolves a clean, adjacent, text-bearing split and safely queues the rest.
  2. **Geometric seam-selector** (`split_geometry.tiling_chains`) cracked the near-identical
     *template* case (bench, pages 138-142): the true children PARTITION the parent (their crop
     bands tile top-to-bottom, abutting at the seam) while look-alikes each fit a full OVERLAPPING
     crop. The neighbour-consistency signal was LATENT in the crop geometry we already computed and
     were discarding — a selection-policy change, NOT the new sequence engine the handoff imagined.
     Real clean SPLIT P66.7/R66.7/silent33 → P100/R66.7/silent0/queue33.
  3. **Degraded OCR-collapse fixture bug fixed** (`scanning.degrade_file` inserted OCR text as one
     blob at one point → degraded splits were degenerate). Now per-word at real positions → real
     degraded SPLIT R0/silent66.7 → R66.7/silent33.
  4. **Visual safety guard** (`split_visual.py`) for the blank-page case (gp): a near-blank,
     text-less parent whose sparse ink REAPPEARS as a crop in the bundle is flagged AMBIGUOUS
     (review), not silent REMOVED. It does NOT resolve gp — the pure-white sibling is unplaceable by
     ANY page-local signal (text, geometry, OR vision) — it just refuses the silent drop.
  The old similarity matchers were ~100% silent because they gated split candidates on whole-page
  *resemblance* (`sim >= tau_floor`), which a fragment can't clear. The stamp is still stripped by
  the real merge ([[mri133-stamp-not-survive-merge]]); pagination still misses split (footer marker
  travels to one child). STILL genuinely open: **gp's confident resolution** (its blank second child
  needs cross-document / sequence evidence — which bundle a blank page belongs to — not page-local
  cleverness). Logged in `IDEAS.md` as the [low] cross-boundary-continuity validators.
- **Pagination channel** (`matchers/pagination.py`, NOT in the default REGISTRY): a high-precision
  partial-coverage channel that reads printed "Page X of Y" as an identity anchor where the marker
  is unique among originals, abstains elsewhere. On real docs: **0% silent / 100% recall on REMOVED**
  (vs perceptual's 67% silent — safety-critical) and resolves **CLONE** confidently. Meant to FUSE
  with the content arm, not stand alone. Rowan PARKED the fuse 2026-07-03 (revisit after the
  coverage-graph reframe); still `[parked] [high]` in `IDEAS.md`.
- **Degraded (scanned) population** is wired into the bake-off (`run --population
  clean|degraded|both`) AND now a valid SPLIT surface (the fixture bug above is fixed). The content
  arm is still weaker on degraded overall (DUPLICATE etc.), but splits now resolve/queue there too.
  `stamped_id` is population-independent. Never quote content-arm numbers clean-only.

- **Coverage-graph reframe DONE (2026-07-03).** The four cardinality cases now live under ONE model:
  `matchers/coverage_graph.py` is a bipartite-IR overlay (`build()` admits edges from the same
  sim/coverage signals, `resolve()` reads outcome off node degree); `decide()` is a thin compat shim;
  token helpers extracted to `matchers/content_tokens.py`. Output-neutral by construction, PROVEN by a
  committed golden fixture (`tests/test_output_neutrality.py`, 2160 predictions identical before/after).
  Hardening (`/harden-plan`) DROPPED the originally-planned capacitated min-cost-flow/ILP backbone: a
  solver computes degree differently from the current code so it couldn't be output-neutral, and the
  report reserves ILP for local clone/split, not the backbone. Do NOT re-propose the solver backbone.
- **Dormant REMOVED margin rule (built 2026-07-03, OFF).** The report's p7 deletion verifier lives in
  `coverage_graph.resolve()` behind dials `removed_coverage_floor` / `removed_margin_min` (both default
  0.0 = no-op, so the pipeline stays neutral). It emits AMBIGUOUS, never a confident REMOVED (a
  confident REMOVED on a present page = silent error). NOT yet validatable (real corpus was silent-0 on
  REMOVED, ~9 pages); its enable-gate is the corpus expansion (now 11 real docs, see
  [[mri133-real-data-container]]): stamp+wire the new docs, calibrate the two dials on the enlarged data
  holding silent-0, then enable or drop.

**How to apply:** SPLIT detection is DONE and the coverage-graph reframe is DONE (the architectural home
for the split logic). Do NOT re-propose more split channels, token/geometry tuning, or the capacitated
solver backbone. The only genuinely open SPLIT gap (gp's blank child) needs cross-document/sequence
evidence, out of page-local scope. The live backlog front is now the **corpus-expansion build** (stamp
the 8 new real docs, wire `scripts/real_bakeoff.py` to source all 11, run, then decide the dormant
REMOVED rule's enable-gate) and the still-parked pagination fuse. When reporting content-arm accuracy,
use the degraded population, not clean. Full record: `docs/DESIGN-NOTES.md` 2026-07-02/07-03 +
`plans/before-numbers/BASELINE.md`; backlog in `docs/IDEAS.md`. Related:
[[mri133-content-arm-scoped-to-originals]], [[mri133-bakeoff-clean-only]], [[mri133-github-remote]].
