---
tags: [medbrief, mri-133, annotations, architecture, advisory]
repos: []
model_check: not-needed
---

# MRI-133 annotation-relocation advisory (2026-06-19)

Advisory session vetting Rowan's Teams exchange with Deon on MRI-133 annotation relocation, grounded in the DB-verified research (notes/14). Confirmed `Page.id` exists only on `BatchDocument`s (minted at sort-prep) and that every annotation today sits on a page-less `Document`; established the replace-vs-sort solution split (content/sequence matching for page-less docs versus `Page.id` rebind-plus-lineage for sorted); named the mechanism and libraries; and recommended a matcher-first v1 that defers `Page.id`-binding.

No files written this session (plan mode throughout). A concurrent session was live in the same repo on MRI-133 (new `notes/15-mri-133-divergent-architectures.md`, +19 lines to `notes/14`, +1 to `docs/SOURCES.md`), all left untouched. This session's synthesis is preserved here; folding it into the notes is a clean follow-up once the concurrent edits land.

## Key points
- **Deon dialogue.** Rowan's sent message was largely correct; sharpened two points (the "those docs never get resorted" assumption was the one unverified claim; all annotations are page-less, not just client uploads). Deon's reply (replace-document + advise-the-user + internal-users-first) is sound. Corrected Rowan's draft: replacing a manual upload does NOT create `Page` records - that belongs to the sort case, not the replace case.
- **Three populations.** Raw / never-sorted uploads (no `Page.id`, content-match only); sorted output (page-less now, the `Page.id` link recoverable at export but not persisted); the internal `Page` layer (has `Page.id`, the core re-sort/lineage problem).
- **Mechanism + libraries.** Page-level sequence alignment over per-page OCR/text fingerprints (difflib / rapidfuzz), a normalised-text hash fast-path, imagehash/perceptual-hash fallback for image-only pages, a confidence threshold driving an advise-and-confirm review tail; Apryse for XFDF read/write and coordinates. Reframe: anchor text highlights to their underlying text so page-count changes stop mattering.
- **Recommendation.** Start with the universal content-matcher (covers ~100% of current annotations, is the fallback the target design needs anyway, and is strictly better than today where references just break). Defer `Page.id`-binding and the non-annotation reference types (chronology, CER index, AI citations).
- **Open product question for Deon/Dion.** Whether the intended future workflow annotates the sorted, paginated output - which would require building the output-page -> `Page.id` connection.
