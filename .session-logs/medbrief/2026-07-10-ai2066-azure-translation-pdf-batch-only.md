---
date: 2026-07-10
project: medbrief-work
domain: medbrief
tags: [ai-2066, azure-translation, document-translation, compre, phi, medbrief-ai, spike]
repos:
  - medbrief-work
model_check: fired-downgrade (model)
---

# AI-2066: Azure translation hands-on, sync refuses PDF (batch-only)

Tested `clinicalrecord-translator` (the deployed Azure Translator, S1/uksouth) directly on the case-44240 sample. The synchronous `document:translate` endpoint translates text, Office and HTML but **refuses PDF** with `InvalidFormat/ContentType` on every api-version, so PDF is **batch-only** and needs blob-container SAS staging. `AI_Shared_Dev` has no storage account and Rowan cannot create one; the only reachable staging account is `stgsalli3odev` (Salli's dev storage, uksouth). Paused on Rowan's decision of where to stage the PHI, then consolidated the finding into `docs/ai-2066/` (SOURCES, DESIGN-NOTES, PLAN, OVERVIEW, BENCHMARK, plus a gitignored `harness/` with a ready batch runner). No run executed; no PHI left the machine.

## Where we left off
- Parked for Rowan: how to stage the PHI for the batch PDF run (options a/b/c/d in `docs/ai-2066/OVERVIEW.md`). The batch harness (`docs/ai-2066/harness/batch_translate.sh <account>`) is ready once an account is chosen.
- Awaiting Laura's ticket reply: which sample pages are German vs the existing English, the Greek attempt, and Google/AWS/DeepL benchmark accounts.
- Design consequence recorded: the translation pass is inherently an async, storage-backed step (the `salli_func` Azure-Function precedent), not an inline call.

## Notes
- The parallel MRI-134 agent is live in the same workspace (`repo/` subrepo and `docs/mri-134/DESIGN-NOTES.md`); left untouched, not committed by this wrap-up.
- Method captured reproducibly in `docs/ai-2066/harness/README.md` (the working sync-text call and the blocked sync-PDF call).
