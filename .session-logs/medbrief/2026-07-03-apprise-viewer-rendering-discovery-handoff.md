---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering
domain: medbrief
session: Discovery, hardened proof plan, and PII fixtures for MedBrief page-subset (date-filter) rendering (MRI-134)
type: handoff
tags: [medbrief, apryse, pdf-rendering, MRI-134, harden-plan, proof-of-principle]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering
    commit: 5192c92
model_check: not-needed
---

## Session Summary

Traced MedBrief's Apryse/XOD viewer end to end and found the founding premise wrong: byte-range streaming already works (`serveAzureBlobRange` returns 206 partial content), so the real task is a page-subset view, not a streaming fix. Hardened a proof-of-principle plan via a six-critic pass (page-list extraction now; date-range split out as a no-build findings spike, because `ChronologyItem` pages are project-level Bates references, not per-document indices), and staged real PII scale-test fixtures under a gitignored `data/`. Work traces to MRI-134; the build moves to a new dedicated MedBrief code project.

## Continuation Prompt

## Continuation: MedBrief page-subset (date-filter) rendering — build the proof (MRI-134)

**Parent session:** 2026-07-03-apprise-viewer-rendering-discovery-handoff.md

### Context
- You are in Rowan's NEW dedicated MedBrief code project (a working copy of the medbrief codebase). This is where the build happens.
- Task: MRI-134 "Date Filter | Filter documents within pdf's by date filter". Deon Kuhn (CTO) asked for a proof of principle: can we, on the fly, return a PDF of only certain pages of a source document? If yes, page-filtering (hence date-range filtering) is proven possible.
- Discovery and a HARDENED plan already exist in a separate TRACKING project (the hub of record). Read them first; do not re-derive, they are grounded in the code.

### Read first (hub of record — separate project, absolute paths)
- Hardened plan:  /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering/docs/PLAN.md
- Findings/decisions: /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering/docs/DESIGN-NOTES.md
- Overview/status:    /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering/docs/OVERVIEW.md
- Sources/fixtures:   /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering/docs/SOURCES.md

### Established findings (verified against the code — do not re-investigate)
1. "Apprise" = Apryse (formerly PDFTron), WebViewer 10.9.
2. Byte-range streaming ALREADY works: XOD is served page-on-demand from Azure Blob over HTTP Range (VichUploaderFileHandler::serveAzureBlobRange returns 206). The "whole doc loads into memory" premise is wrong. This is a page-SUBSET feature, not a streaming fix.
3. Extraction tooling exists: PDFTronSplitPdf (InsertPages), PDFTronMergePdf. InsertPages has a PageSet overload (PDFNetPHP_core.php:16563), already used in PDFTronStamperService.
4. BLOCKER for date-range: ChronologyItem -> Chronology -> Project (no Document FK). Its pageFrom/pageTo are project-level Bates references (nullable strings, e.g. "GP000123") into the collated matter bundle, NOT indices into the single document the viewer shows.

### Decision (from the hardened plan)
- Lightweight viewer path. Build page-LIST extraction now (Workstream A). Date-range is split out as a no-build findings spike (Workstream B) because of the blocker above.
- Safe defaults: serve behind existing project+document security; disable download/print in the preview; hand-pick a clean single-document record for the demo; no cache.

### Current state
- Tracking-project docs committed at 5192c92.
- Fixtures staged (gitignored, PII, real medical records — DO NOT OPEN) at:
  /Users/Rowan.Reid/claude_code/projects/apprise-viewer-rendering/data/real-samples/
  Ladder: 144017-12303 (32pp), combined_108815 (142pp), combined_100200 (242pp), combined_118830 (403pp), 691c7696...pdf (1344pp, ~261MB). Byte-weight pair: combined_115131 (168pp/9MB) vs combined_115132 (172pp/19MB). Heavy stressor: 142257-12147 (342pp/165MB).
- Sibling medbrief clones (medbrief-onboarding/repos, data_pipelines) are REFERENCE ONLY. Build in THIS project's copy.

### Next steps (Workstream A, in order)
0. Confirm with Rowan: prototype extraction as a standalone script first (fastest path to the scaling answer), or build straight into the app? Recommendation: standalone prototype first.
1. Extraction method: add extractPagesByPageNumbers(path, int[] pages, outputPath) to SplitPdfInterface + PDFTronSplitPdf, using ONE InsertPages(0, $doc, new PageSet(...), e_none) call; save linearised; do NOT force-flatten (destroys text); guard div-by-zero on a 0-page source; decide on the >100MB hard-abort. Unit-test ordering/dedupe/out-of-range. (PLAN step 2)
2. Page-spec parser: "5,12,30-35" -> sorted unique 1-based ints; validate 1<=p<=pageCount; reject empty/non-numeric/reversed; cap total span. (step 3)
3. Endpoint: streamPageSubsetAction in ProjectDocumentController; route infology_medbrief_project_document_stream_page_subset at /{documentId}/stream-page-subset/{filename} with {id}+{documentId} ParamConverters; gate is_granted('READ',project) && is_granted('STREAM_NATIVE',document); resolve source via PathResolverStrategy::resolvePdfDirectoryPath (ocr>optimized>native), materialise locally before PDFNet; Cache-Control: private,no-store; dedicated audit verb; never expose a blob SAS URL. (step 4)
4. Lightweight preview: pdf.js with toolbar/download/print disabled, same-origin, under the app's real CSP. (step 5)
5. Scale test (the key measurement): hold subset fixed (40 pages), VARY source size across the fixture ladder; cold vs warm; scattered vs contiguous; record extraction latency + peak RSS + output bytes, and client TTFB + time-to-first-rendered-page (p50/p95); run through the real blob path. (scale-test redesign)
6. Demo + record numbers back in the tracking project's DESIGN-NOTES.md.

Workstream B (no build): investigate how ChronologyItem Bates pages map to a document + local page index (collate_before_processing, paginationType/Prefix/Strategy); write a findings note for Deon naming the prerequisite for a real date-range feature.

### Key references (code anchors)
- src/Service/PDFTools/Split/PDFTronSplitPdf.php (InsertPages, extractSinglePageByPageNumber)
- src/Service/PDFTools/PDFNet/PDFNetPHP_core.php:16563 (InsertPages PageSet overload)
- src/Service/PDFTools/Stamper/PDFTronStamperService.php (PageSet precedent)
- src/Service/PDFTools/Merge/PDFTronMergePdf.php
- src/Controller/ProjectDocumentController.php (stream* actions: security + once-only audit)
- config/routing/project-document.yml (stream route naming)
- src/Service/File/FileHandler/VichUploaderFileHandler.php (serveAzureBlobRange, copyToLocal)
- src/Service/PDFTools/PathResolver/PathResolverStrategy.php (resolvePdfDirectoryPath)
- src/Entity/ChronologyItem.php, src/Entity/Chronology.php (date-range blocker)
- Jira: https://medbrief.atlassian.net/browse/MRI-134

### Notes for next session
- PII discipline: fixtures are real medical records. Never open/read content; keep derivatives gitignored; for page counts use a content-free method (qpdf --show-npages, or pdfinfo grepping only the Pages line).
- Discovery was verified against medbrief `main` @ dc33139b5. Confirm this project's checkout is current before trusting line numbers.
- Model/effort: architecture/build work — opus/high or xhigh is appropriate.
