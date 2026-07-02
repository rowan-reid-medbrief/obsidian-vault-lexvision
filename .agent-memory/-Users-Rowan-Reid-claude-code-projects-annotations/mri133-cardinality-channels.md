---
name: mri133-cardinality-channels
description: "What each matcher channel can and cannot do on the hard cardinality cases (split/clone/removed/inserted); SPLIT is now PARTIALLY solved (token-space containment->set-cover->adjacency + a geometric crop-residual substrate resolve clean adjacent text splits; near-identical template and blank-page splits remain); degraded population collapses the content arm"
metadata:
  type: project
  originSessionId: this-session
---

The MRI-133 matchers are one-to-one assignment machines; they break on **cardinality
changes** (a page becoming several, or none, or an inserted page). Measured reach (2026-07-02,
on the 3 real Azure docs and the synthetic corpus):

- **SPLIT is now PARTIALLY solved (was: unsolved by every channel).** Acting on the commissioned
  deep-research report — splits are a *containment* problem, not a *resemblance* one (Broder) — a
  token-space pipeline in `decision.py` (containment selection → greedy weighted set-cover →
  adjacency guard) took real clean SPLIT from **100% silent → 33% silent, 50% recall / 60%
  precision**: it confidently resolves a clean, adjacent, text-bearing split (distinct content) and
  safely queues the rest. A geometric substrate (`matchers/split_geometry.py`: RANSAC
  translation+scale CROP fit over distinctive word boxes) filters look-alikes by transform residual
  and supplies the real source-region bands for annotation transfer; it holds the metric and
  generalises past the adjacency heuristic. The old similarity matchers were ~100% silent because
  they gated split candidates on whole-page *resemblance* (`sim >= tau_floor`), which a fragment
  can't clear; the stamp is still stripped by the real merge ([[mri133-stamp-not-survive-merge]]);
  pagination still misses split (footer marker travels to one child). STILL UNSOLVED by page-local
  evidence: **near-identical template pages** (all fit a crop of the parent, so neither token overlap
  nor crop residual separates the true children — needs sequence / neighbour-consistency context) and
  **blank/near-blank pages** (no text — needs the visual channel). Both logged in `IDEAS.md`.
- **Pagination channel** (`matchers/pagination.py`, built this session, NOT in the default
  REGISTRY): a high-precision partial-coverage channel that reads printed "Page X of Y" as an
  identity anchor where the marker is unique among originals, abstains elsewhere. On real docs:
  **0% silent / 100% recall on REMOVED** (vs perceptual's 67% silent — safety-critical) and
  resolves **CLONE** confidently (the content arm could only queue). 0.1% silent overall. Meant
  to FUSE with the content arm, not stand alone. Reach depends on provenance: source-doc
  pagination lives on `Page.pdfFile` originals (viable for internal re-sorts); a monotonic 1..N
  run is MedBrief's export burn (bundle only). Next step: fuse it into the ensemble (`IDEAS.md`).
- **Degraded (scanned) population** is now wired into the bake-off (`run --population
  clean|degraded|both`). Clean → degraded: the content-arm ensemble goes GOOD → POOR (silent
  3.2% → 22.3%); `exact_hash` and `text_fingerprint` collapse similarly; **`stamped_id` is
  unchanged** (population-independent). This is the number behind "only the stamp is robust";
  never quote content-arm numbers clean-only.

**How to apply:** the split-detection approach is now proven and built (containment → set-cover →
adjacency, plus a geometric crop-residual substrate); don't re-propose pagination or the stamp for
split. The two remaining SPLIT gaps are near-identical *template* pages (needs sequence/neighbour
context) and blank pages (needs the visual channel) — NOT more token/geometry tuning. Pagination
fusion into the content arm (for REMOVED safety + CLONE) is still open. When reporting content-arm
accuracy, use the degraded population, not clean. Full record: `docs/DESIGN-NOTES.md` 2026-07-02
(three SPLIT entries) + `plans/before-numbers/BASELINE.md`; backlog in `docs/IDEAS.md` 2026-07-02.
Related: [[mri133-content-arm-scoped-to-originals]], [[mri133-bakeoff-clean-only]].
