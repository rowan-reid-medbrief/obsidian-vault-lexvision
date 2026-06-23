---
date: 2026-06-23
project: annotations
domain: medbrief
session_id: e4bd9847-76f4-4fb8-997f-430421128711
tags: [mri133, milestone-b, annotations, relocation, geometry, xfdf, apryse, python-sdk]
commits:
  annotations: 8b3be7e
model: claude-sonnet-4-6
effort: high
---

# Session: MRI-133 b1 — Relocation Core
2026-06-23 | annotations | medbrief

Built the full annotation relocation core for Milestone B of the MRI-133 PoC.

## What shipped

- apply/geometry.py: intersection, overlap_fraction, reproject_to_child, clamp_rect, rect_valid (pure Python, no Apryse dependency)
- apply/xfdf.py: parse_xfdf, rewrite_page, rewrite_pages, build_xfdf, filter_by_page (ElementTree XML-level page attribute rewrite; preserves namespaces and encoding)
- apply/relocate.py: full Outcome dispatch — MATCHED (atomic move), REMOVED (to review queue), CLONED (duplicate per placement), SPLIT (reproject to all overlapping children via reproject_to_child), AMBIGUOUS/NO_MATCH (abstain to queue)
- pdfnet.py: APRYSE_SDK_SKIP guard, WebViewer-vs-server-SDK diagnostic (clear error message), idempotent init
- apply/merge.py: import_xfdf and export_xfdf via FDFMerge (gated on SDK key)
- poc/src/mri133/cli.py: mri133 demo subcommand skeleton
- Index-base round-trip test, cross-authority enforcement test (no module may repin PAGE_INDEX_BASE)
- 71 new tests; 162 passed / 3 skipped (3 FDFMerge smoke tests skipped pending Python SDK key)

## Key finding: Apryse WebViewer key vs Python server SDK

The trial key in .env (demo:deon@sideclick.co.za:...) is the Apryse WebViewer (JavaScript) key. The Python server SDK (apryse-sdk >= 11) requires a different key format. PDFNet.Initialize() rejects the WebViewer key with "This product must be initialized with a valid key."

Searched Confluence and the MedBrief codebase for a Python SDK key:
- The PHP monolith uses the WebViewer key for both WebViewer and the PHP PDFNet binding (more lenient than Python v11)
- A Python OEM key from 2019 was found in git history but expired January 2020 and was intentionally removed (MB-322)
- The Windows nameko service uses PDFTRON_LICENSE stored in Windows system env only, never committed

Resolution: Deon must obtain a fresh Python server SDK trial key from dev.apryse.com. The FDFMerge smoke test will run once that key is in .env as APRYSE_LICENSE_KEY.

## Open items

- FDFMerge smoke test: 3 tests in test_fdfmerge_smoke.py SKIPPED. Pending Python SDK key from Deon.
- If ink annotation test fails: implement per-subtype delete+recreate in apply/merge.py.
- b2 session: blocked on b1 FDFMerge confirmation + Python SDK key.
