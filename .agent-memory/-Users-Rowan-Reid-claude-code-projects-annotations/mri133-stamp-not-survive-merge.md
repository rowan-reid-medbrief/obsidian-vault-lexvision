---
name: mri133-stamp-not-survive-merge
description: "Spike result (2026-07-02): a custom in-PDF page-dictionary stamp does NOT survive MedBrief's real PDFTron merge on either path (PagePushBack or flatten); use the DB Page.id instead"
metadata:
  type: project
  originSessionId: this-session
---

The a1 spike (2026-06-23) showed a `/MRI133Id` page-dict key survives a pikepdf/pymupdf
save+repaginate, and the June design leaned on "stamp a durable id at extraction". A
follow-up spike (`poc/spikes/stamp_survival_pdftron.py`) tested MedBrief's **actual** merge
tool with the Apryse/PDFTron Python SDK and found the stamp does **not** survive:

- `PagePushBack` (normal A4 page — the previously-open, previously-assumed-safe case): **LOST**,
  confirmed by two independent read channels (pikepdf + Apryse SDF).
- flatten branch (undersized page, rasterise-and-rebuild): LOST (already expected).
- Control (bare `open + Save(e_compatibility)`, no merge): SURVIVED.

So the loss is specifically the cross-document `PagePushBack` import discarding a foreign
page-dictionary entry (PDFTron copies standard page structure + content, not arbitrary custom
keys). Page **content** survives the merge intact; only the custom key is dropped.

**Why:** this partially refutes the naive "stamp the PDF" durable-id design. It does NOT
reverse the stamp-first *scope* decision — for internal original-vs-original matching the id
sits on the never-merged `Page.pdfFile` and is safe (see [[mri133-content-arm-scoped-to-originals]]).
It rules out relying on an in-PDF stamp to re-identify pages *inside an exported bundle* — which
is exactly the 12-25% sorted-and-annotated population ([[mri133-annotations-not-confined-to-unsorted]]),
so content/pagination-based cardinality detection matters more for that population.

**How to apply:** treat the durable id as the DB `Page.id` keyed to the stable `Page.pdfFile`
asset, not a key planted in the PDF. An in-PDF stamp is only needed if a document must leave
MedBrief and return, and a page-dict key is the wrong mechanism there (PDFTron discards it) —
it would need visible content-stream text (like MedBrief's own page-number burn) or XMP. Full
record: `docs/DESIGN-NOTES.md` 2026-07-02 "Stamp-survival vs the REAL merge"; trace
`docs/research/mri-133-research.md` §14.2; `docs/research/mri-133-divergent-architectures.md` §8/§9 item 5.
