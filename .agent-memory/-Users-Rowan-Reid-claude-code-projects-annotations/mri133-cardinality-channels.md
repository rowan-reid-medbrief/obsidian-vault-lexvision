---
name: mri133-cardinality-channels
description: "What each matcher channel can and cannot do on the hard cardinality cases (split/clone/removed/inserted). The 11-doc real corpus surfaced 3 silent SPLIT errors the 3-doc corpus had HIDDEN (correcting the earlier 'zero silent both populations' claim): 2 = image-only pages (retired by in-matcher OCR, ad0f125), 1 = an exact-duplicate twin split (bench-115132, safe-queued via twin_split_abstain 2026-07-03). With both, SPLIT returns to zero silent on the real corpus. Open gaps (RESOLVING, not just safe-queuing): exact-duplicate + cross-section splits need sequence/neighbour context, not page-local evidence; gp's blank child. Pagination fuse parked. 2026-07-05: blanket median fusion (Lever A) FAILED its real-corpus safety gate; a mean-primary/median-rescue hybrid shipped instead (safe, DoD still MARGINAL)."
metadata:
  type: project
  originSessionId: this-session
---

**UPDATE 2026-07-05 (supersedes the "sequence layer is the lever" framing below).** The
sequence/neighbour layer was investigated and CUT. The ceiling read + a corpus-wide go/no-go
(`plans/2026-07-04-sequence-layer-*.md`) showed the review queue is BIMODAL: docs are either
well-anchored (already resolve 97-100%) or fully content-unresolvable (bench-115131: 168pp, 22
distinct texts, 42 blanks, 0 unique-placement anchors on EVERY channel), with an EMPTY resolvable
middle - so a neighbour-bracketer has nothing to bracket (0 bracketable pages across 8 text docs).
The actual queue fix is **Lever A: median fusion** (per-cell median of exact_hash/perceptual/
text_fp = trust a 2-of-3 agreement), which converts every weak-match over-abstain (fused ~0.667
under the old equal-weight MEAN, below tau_accept 0.80) to a confident anchor (measured 108->0). It
leaves genuinely identical pages ABSTAINED (all 3 channels tie -> no false confidence). Repetitive/
blank docs are information-theoretically content-unresolvable = the durable stamp's territory (a Deon
finding). Plan hardened via /harden-plan (13 critics; the key catch: "precision >= 0.95" tolerates
~555 PII mis-transfers, so the ship gate is now an ABSOLUTE zero-new-silent-error count on the FULL
population). STILL TO BUILD: Lever A (a `fusion_rule` dial, default-on + `_NEUTRAL_CFG` pin-mean) +
its two safety gates (a synthetic dial-ON DUPLICATE/removed-look-alike archetype run + a real-corpus
zero-new-silent bake-off). The "open gaps" / "sequence/neighbour layer" framing in the body below is
now historical context, not live work.

**UPDATE 2026-07-05 (later session) - Lever A as a BLANKET rule FAILED; a mean-primary/
median-rescue hybrid shipped instead.** Built `fusion_rule` (config.py) exactly as the update
above specified. Its real-corpus safety gate (`scripts/lever_a_safety_gate.py`) FAILED: 1 new
distinct SILENT_ERROR id (real-bench-115132#0086, composed_resort) and a hard DoD regression
(recall 0.6727->0.5895, queue 0.3267->0.4098), concentrated almost entirely in PLAIN (-923
CONFIDENT_CORRECT) and REPAGINATION (-299) - the OPPOSITE direction the small-scale probe
(108->0) predicted. Mechanism: the near-tie check (`decision.py:243`) reads the RAW fused `sim`
row, not the IDF-weighted `content_frac`, so median protects a WRONG candidate's score from a
correctly-dissenting third channel exactly as much as the RIGHT one's - on boilerplate-heavy real
documents (shared header/footer/patient-info) that manufactures far more false near-ties than it
resolves. Rowan's redesign choice: a mean-primary/median-rescue hybrid
(`config.median_rescue_enable`, upgrade-only - mean decides every page unconditionally; only a
page mean sends to AMBIGUOUS gets a second look under median, adopted only if median's own
independent re-classification is a clean MATCHED). Its real-corpus gate
(`scripts/median_rescue_safety_gate.py`) PASSED clean: zero new silent errors, +48 pages resolved
(recall 0.6727->0.6760, queue 0.3267->0.3234), the gain concentrated in the SAME PLAIN/
REPAGINATION case types the blanket rule broke, this time safely. **DoD still MARGINAL, not
GOOD** (recall/queue both short of the 0.70/0.30 bar) - a safe, small step, not a resolution of
the queue. Also found: bench-115132 is a fully repetitive-TEMPLATE doc (122/172 exact-twin
pages), NOT image-only (correction logged in [[mri133-real-data-container]]).
`poc/scripts/content_ceiling.py` is the honest, GT-free per-doc ceiling read for Deon. Lesson for
any future global-signal change: a small-scale/synthetic probe can validate the wrong mechanism
entirely - only the full real-corpus scored run surfaced the near-tie-inflation effect.

The MRI-133 matchers are one-to-one assignment machines; they break on **cardinality
changes** (a page becoming several, or none, or an inserted page). Measured reach (2026-07-03,
on the 3 real Azure docs and the synthetic corpus):

- **SPLIT: zero silent errors on the real corpus (CORRECTED framing).** The earlier "zero silent both
  populations" held only on the 3-doc corpus; the 11-doc corpus surfaced 3 silent SPLITs it had hidden,
  retired by TWO ADDED mechanisms (points 5-6 below): OCR for image-only pages, safe-queue for
  exact-duplicate twins. The original token/geometry arc, all acting on the commissioned
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
  5. **In-matcher OCR** (`io/ocr.py`, `ad0f125`): an image-only page (salli-142257, 342/342 text-less)
     is invisible to every content signal, so a split of it read as silent REMOVED. OCR just the
     text-less pages before matching. Retired 2 of the 3 silent SPLITs the enlarged corpus surfaced.
     OCR is content-address-cached (`b4172f9`) AND (2026-07-04, `2804882`) subprocess-isolated with a
     per-page wall-clock timeout (`ocr_page_timeout_s`=120s, SIGTERM+skip) - the OCR HANG is RETIRED
     (confirmed in-situ: a curated clean bake-off hit the pathological page, timed out, skipped, completed).
     The matcher per-page RENDER wall is retired (2026-07-04, `0505505` for the matcher arm; the OCR-arm
     render was ALSO routed through the same content-addressed cache 2026-07-04 via `render_png_cached`,
     closing a 9x cross-scenario re-render redundancy - byte-identical, 316 tests). CORRECTION (2026-07-04):
     the parent's `[high]` "sliver -> 120s OCR timeout" blowup was DISPROVEN - real geometric slivers OCR in
     0.4s, real scan pages 0.6-1.7s, only 2/8 scenarios split (one page each), and a 1-in-4 sample of the
     capped range found 0 timeouts. The real full-run cost is MATCHER-ARM compute (~44 min of a 56-min capped
     clean run), NOT OCR/slivers. FULL-CORPUS CLEAN CONFIRMATION COMPLETED (2026-07-04, `--cap-pages 200`, the
     run the parent aborted): content-arm ensemble SPLIT 4.5% silent / 45.5% queue vs the render/OCR-INDEPENDENT
     stamped arm's 36.4% silent -> NO OCR-induced content-split regression (the content arm handles SPLIT
     BETTER, by queueing). Ensemble DoD MARGINAL: P99.9 / R69.0 / queue31.0 (recall + queue miss the proposed
     bars by ~1pt; the sequence layer is the lever).
  6. **Exact-duplicate twin safe-queue** (`twin_split_abstain`, `coverage_graph.py`, 2026-07-03): a
     split page whose EXACT duplicate survives whole (bench-115132 171/85: byte-identical text AND
     geometry, split residual 0.00000) was silently MATCHED to the duplicate. No page-local signal can
     separate the cut copy from its twin (information-theoretic); letting the split COMPETE just
     relocated the error (measured silent 1→1). So a confirmed reconstruction coinciding with a
     CONTESTED full holder is safe-queued (AMBIGUOUS) — removing the silent error without relocating it,
     gated on a confirmed reconstruction so plain duplicates aren't queued (surgical: silent 1→0, zero
     collateral; monotone-safe — only ever emits AMBIGUOUS). RESOLVING which copy was split needs the
     sequence layer, not page-local evidence. Drove [[mri133-content-arm-primary-goal]].
  The old similarity matchers were ~100% silent because they gated split candidates on whole-page
  *resemblance* (`sim >= tau_floor`), which a fragment can't clear. The stamp is still stripped by
  the real merge ([[mri133-stamp-not-survive-merge]]); pagination still misses split (footer marker
  travels to one child). STILL genuinely open, TWO gaps:
  (a) **Cross-section (non-adjacent) confident resolution.** The adjacency guard (`split_require_adjacent`)
  only auto-places a split whose children are CONTIGUOUS; a real "scatter re-sort" that files a split
  page's halves into different clinical sections is safely QUEUED, not resolved (fails safe, not solved).
  Our two real split cases (salli 31+32, bench 141+142) were both adjacent, so this is untested. Fix
  direction: the geometric shape-fit channel does NOT need adjacency, so relax the adjacency requirement
  and lean on geometric residual + coverage (and/or make the matcher clinical-section-aware). Surfaced by
  Rowan 2026-07-03; logged as a `[high]` idea + its `[high]` cross-section test fixture.
  (b) **gp's confident resolution** (its blank second child needs cross-document / sequence evidence —
  which bundle a blank page belongs to — not page-local cleverness). Logged as the [low]
  cross-boundary-continuity validators.
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

**How to apply:** SPLIT detection is DONE for ADJACENT splits and the coverage-graph reframe is DONE (the
architectural home for the split logic). Do NOT re-propose more split channels, token/geometry tuning, or
the capacitated solver backbone. But TWO SPLIT gaps ARE sanctioned open work (do not dismiss them as
"splits are done"): **cross-section (non-adjacent) confident resolution** (the `[high]` idea + its test
fixture, 2026-07-03), **RESOLVING (not just safe-queuing) the exact-duplicate twin split** (point 6 —
needs the sequence layer, same lever), and **gp's blank child** (cross-document/sequence evidence, out
of page-local scope). The corpus-expansion build is DONE (11 real docs stamped + wired into
`scripts/real_bakeoff.py`); the remaining fronts are the **sequence/neighbour layer** (the common
"resolve near-identical pages" need behind cross-section + exact-duplicate + gp), the dormant REMOVED
rule's enable-gate, and the still-parked pagination fuse. When reporting content-arm accuracy,
use the degraded population, not clean. Full record: `docs/DESIGN-NOTES.md` 2026-07-02/07-03 +
`plans/before-numbers/BASELINE.md`; backlog in `docs/IDEAS.md`. Related:
[[mri133-content-arm-scoped-to-originals]], [[mri133-bakeoff-clean-only]], [[mri133-github-remote]].
