---
name: mri133-bakeoff-clean-only
description: "The MRI-133 bake-off scores the clean corpus only; the degraded (scanned) variant is unused, so headline numbers are the easy-population best case."
metadata: 
  node_type: memory
  type: project
  originSessionId: 285f01fd-a836-44ba-afe3-a138d5010f9b
---

The `mri133 run` bake-off currently matches and scores the **clean** (born-digital) corpus only. The generator produces a `.degraded.pdf` (image-only + ~6% corrupted OCR text) per document and stamps it with the same page ids, but nothing in `mutate/`, `matchers/`, or `scoring/` ever reads `degraded_path` (`scorer.py` mutates and matches `gd.clean_path`).

**Why it matters:** the reported content-arm numbers (e.g. `exact_hash` P 92.9%) are measured on identical digital text against itself, so they are an optimistic, best-case read. On real scanned bundles the content matchers would do clearly worse (their five perfect per-scenario scores depend on byte-identical text). Be honest about this with Deon: it means the content-matching numbers flatter reality, which if anything strengthens the stamp-at-extraction case. Wiring the degraded variant into the bake-off (e.g. a `--population clean|degraded|both` flag) is the tracked next build. See [[mri-133-project]].
