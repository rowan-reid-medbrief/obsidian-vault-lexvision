---
name: mri133-content-arm-scoped-to-originals
description: "Content-arm (exact_hash/perceptual/text_fingerprint) matching should compare pre-pagination originals, never exported/stamped bundles — resolves the repagination-poisons-matching concern"
metadata: 
  node_type: memory
  type: project
  originSessionId: 62d479c6-b8dc-42c6-b2e0-b07d564b17c0
---

MedBrief re-stamps a visible page number onto every export (three-layer trace:
`PaginatePagesMiddleware` recomputes position -> number; `MergePagesMiddleware` overwrites
`Page.pageNumber` in the DB; `PDFTronStamperService::applyPageNumbers` burns it onto the
merged PDF via PDFTron `StampText`, real content-stream text, not a removable annotation).
This looked like it would poison `exact_hash`-style matching on any resort.

It doesn't, once scoped correctly. `Page.pdfFile` (the original per-page asset each `Page`
row carries) is **never mutated** by pagination, merging, stamping, or the flatten step
production runs for undersized pages — confirmed from `PDFTronMergePdf::merge()`, which
copies the file to a `.flat.pdf` path before rasterising, never touching the source. Any
resort happening inside MedBrief builds both the old and new arrangement from this same
kind of never-repaginated original, so content-arm matching should always compare
original-vs-original (fetched by `Page.id`), never bundle-vs-bundle. The visible burn then
never enters the comparison.

**Why:** this was going to shape a chunk of PoC test design (a mutation-engine change to
simulate the burn, so `exact_hash` numbers reflected "reality"). That framing was
backwards — the PoC's corpus already never stamps anything, which is the *correct* design,
not a gap. Fixing this saved building the wrong test.

**Second finding, same trace:** MedBrief's real merge tool has two paths. A normal-width
page survives via PDFTron `PagePushBack` (still unverified against the real SDK — a
concrete next spike). A page narrower than A4 (595pt) is rasterised to a PNG and rebuilt as
a fresh PDF first — a **confirmed, deterministic** destruction of any custom page-dictionary
key on that specific export copy (the original `Page.pdfFile` is unaffected, per above).

**How to apply:** any future matcher/testing work should source both sides of a content
comparison from `Page.pdfFile` (or split/clone children of it), never from an exported,
merged, stamped document. Content-arm's real, still-open reliability ceiling is split
geometry, clone disambiguation, and scan degradation — not pagination. See
`docs/research/mri-133-research.md` §14 for the full trace and
`docs/research/mri-133-divergent-architectures.md` §8/§9/§10 for how it changes the fork
and the ranked spike list. Related: [[mri133-annotations-not-confined-to-unsorted]].
