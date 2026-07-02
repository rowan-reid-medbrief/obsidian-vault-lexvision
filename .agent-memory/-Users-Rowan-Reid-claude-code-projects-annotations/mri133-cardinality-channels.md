---
name: mri133-cardinality-channels
description: "What each matcher channel can and cannot do on the hard cardinality cases (split/clone/removed/inserted); SPLIT is unsolved by ALL channels including pagination; degraded population collapses the content arm"
metadata:
  type: project
  originSessionId: this-session
---

The MRI-133 matchers are one-to-one assignment machines; they break on **cardinality
changes** (a page becoming several, or none, or an inserted page). Measured reach (2026-07-02,
on the 3 real Azure docs and the synthetic corpus):

- **SPLIT is unsolved by EVERY channel.** Similarity matchers are ~100% silent on it; the DB/PDF
  stamp is stripped by the real merge ([[mri133-stamp-not-survive-merge]]); and the new
  pagination channel misses it too — the "Page X of Y" marker sits in the footer, so a
  content-balanced split carries it to only ONE child (verified) and pagination reads a plain
  match. Candidate approaches NOT yet tried: adjacency + geometric complementarity (two adjacent
  pages whose regions tile one parent), and reading-order/text-flow continuity across the seam.
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

**How to apply:** don't propose pagination (or the stamp) as a SPLIT fix — split needs a
geometry/continuity approach. Do treat pagination as the fuse-in fix for REMOVED (safety) and
CLONE. When reporting content-arm accuracy, use the degraded population, not clean. Full record:
`docs/DESIGN-NOTES.md` 2026-07-02 "Content-arm reach"; backlog in `docs/IDEAS.md` 2026-07-02.
Related: [[mri133-content-arm-scoped-to-originals]], [[mri133-bakeoff-clean-only]].
