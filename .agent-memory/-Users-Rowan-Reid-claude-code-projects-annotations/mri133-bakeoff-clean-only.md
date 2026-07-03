---
name: mri133-bakeoff-clean-only
description: "The MRI-133 bake-off now matches BOTH clean and degraded populations (--population flag); content-arm numbers are still the clean best case, so quote degraded when reporting to Deon. The degraded OCR-collapse fixture bug (which made degraded splits degenerate) was fixed 2026-07-03."
metadata: 
  node_type: memory
  type: project
  originSessionId: 285f01fd-a836-44ba-afe3-a138d5010f9b
---

The `mri133 run` bake-off now matches and scores BOTH the **clean** (born-digital) and the
**degraded** (image-only + ~6% corrupted OCR) populations, selected by `--population clean|degraded|
both` (`scorer.run_bakeoff` `population` param). This corrects the original state of this memory,
when nothing read `degraded_path` and only the clean corpus was scored.

**Two things to keep honest:**
1. **Content-arm numbers are still the clean best case.** The clean population is byte-identical text
   against itself, so `exact_hash`/`text_fingerprint` score optimistically; on the degraded (scan-like)
   population they drop clearly, while `stamped_id` is population-independent. Be honest with Deon: the
   content-matching numbers flatter reality, which if anything strengthens the stamp-at-extraction case.
   Never quote content-arm accuracy clean-only.
2. **The degraded fixture had a bug, now fixed (2026-07-03).** `scanning.degrade_file` used to insert
   the corrupted OCR layer as ONE blob at a single point, collapsing every token to one y-position, so
   degraded SPLIT was 100% silent as an ARTEFACT (not a real ceiling). Fixed to per-word placement at
   real positions; degraded splits are now genuinely matchable (real degraded SPLIT R0 → R66.7). So
   degraded-population split/spatial-coverage numbers are now meaningful, where before this date they
   were measuring a degenerate fixture. See [[mri133-cardinality-channels]], `docs/DESIGN-NOTES.md`
   2026-07-03. Related: [[mri-133-project]].
