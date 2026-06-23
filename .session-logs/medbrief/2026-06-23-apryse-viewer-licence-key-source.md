---
date: 2026-06-23
project: /Users/Rowan.Reid/claude_code/medbrief-onboarding
domain: medbrief
session: Located the Apryse viewer licence key in the MedBrief monolith and seeded the annotations PoC dev-setup
type: wrap-up
tags: [medbrief, apryse, pdftron, webviewer, records-viewer, mri-133, annotations, dev-setup, secret-leak]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-onboarding
    commit: 45a8e59964f0793f09c56f8236a1fc4fca1db7ec
model_check: not-needed
---

## Session Summary

Traced where the Apryse (formerly PDFTron) WebViewer licence key lives in the MedBrief Symfony monolith (`~/claude_code/projects/data_pipelines/medbrief`): the front-end key is the env var `PDFTRON_WEBVIEWER_LICENSE`, read by `webpack.config.js` into `assets/js/RecordsViewer/index.js`, with a separate server-side PDFNet key bound via `pdftron_sdk_license_key` into `PDFNetSingleton.php`; the committed default is a `demo:` trial key on Deon's Apryse account. Wrote a `docs/dev-setup.md` note in the cousin annotations project (indexed in its SOURCES) documenting how to source the same key for the MRI-133 PoC; Rowan then scrubbed the literal key from that doc in favour of a git-ignored `.env` pointer. Logged two onboarding backlog items: a high-priority storybook-static committed-secrets leak to raise with Deon, and a low-priority cross-ref of the viewer-key wiring into `notes/04`.
