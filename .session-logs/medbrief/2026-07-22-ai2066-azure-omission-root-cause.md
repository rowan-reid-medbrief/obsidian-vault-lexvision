---
session_id: [081104ee-73f3-4233-8ad2-70e00195c66e]
date: 2026-07-22
project: /Users/Rowan.Reid/claude_code/medbrief-work
domain: medbrief
session: AI-2066 Phase 3 item 1, re-confirmed Azure's silent omission against the 2026-03-01 backend and root-caused it as a document-path segmentation bug
type: wrap-up
tags: [ai-2066, azure, translation, medbrief, root-cause, investigation, compre]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-work
    commit: 052c65a513437513f0f169618ae8b120bfe86352
model_check: not-needed
---

## Session Summary

Ran AI-2066 Phase 3 item 1: re-confirmed Azure's silent omission against the current 2026-03-01 backend (routing is tied to the API-version string; the digital path drops content on both backends; the newer backend also regresses the scanned path), then root-caused it. The loss is not the translation engine and not PDF-specific: it is a document-path sentence-segmentation bug triggered by a date-terminated sentence followed by a participial continuation (isolated with controlled DOCX probes, each fix reproduced twice), and the synchronous text path is immune, which turns the DESIGN-NOTES §18 text-layer branch into the safer choice on engineering grounds. Cross-checked against Microsoft's known-issues page and community reports, wrote a minimal non-PHI repro for a support ticket, and prepped a succinct Deon meeting brief (Azure verdict, vendor-vs-architecture point, cited third-party shortcomings).
