---
date: 2026-07-02
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: DB-confirmed a correction to the June MRI-133 annotation-population conclusion, traced the export mechanism
type: wrap-up
tags: [mri-133, annotations, medbrief, docsorter, pagination, content-matching, db-verification]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: b7a1163e304420b22a7a98b52c77d81a10ee5add
model_check: unknown
---

## Session Summary

DB-confirmed a correction to the June MRI-133 research: 12.1-25.4% of annotated documents (445 matters, 31 with a live sort-then-annotate-then-resort sequence) are DocSorter-exported bundles, not raw never-sorted records as previously concluded, contradicting the "annotation essentially never happens on sorted output, 1 of 5,536" finding (which was measuring a signal - `BatchDocument` link, current collection membership - that doesn't survive export). Traced MedBrief's export/pagination mechanism (`PaginatePagesMiddleware` -> `MergePagesMiddleware` -> `PDFTronStamperService`) and its real merge tool (`PDFTronMergePdf`/`PDFTronFlattenPdf`), finding content-arm matching should compare pre-pagination `Page.pdfFile` originals rather than exported/stamped bundles - resolving the repagination-vs-matching concern and correctly vindicating the PoC's existing mutation engine over a previously-proposed change to simulate the visible page-number burn. Propagated the correction across `mri-133-research.md` (new section 14), `mri-133-divergent-architectures.md` (sections 8-10), the vault decision note, `DESIGN-NOTES.md`, `IDEAS.md`, `OVERVIEW.md`, project memory, and the regenerated branded export.
