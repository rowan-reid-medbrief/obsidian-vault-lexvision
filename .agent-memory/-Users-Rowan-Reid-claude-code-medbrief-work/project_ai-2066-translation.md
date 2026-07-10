---
name: ai-2066-translation
description: AI-2066 Compre translation spike; Azure sync refuses PDF (batch-only), storage-provisioning gap; paused on staging decision
metadata:
  type: project
---

Azure DevOps work item **2066** (MedBrief AI project), a Compre translation and pseudonymisation workflow spike assigned to Rowan. Full working detail in `docs/ai-2066/`; vault thread in `Next Up.md` under `## Now (Medbrief)`.

Two non-obvious findings from the 2026-07-10 hands-on test, expensive to re-derive:

- **Azure Document Translation refuses PDF on the synchronous endpoint** (`document:translate` returns `InvalidFormat/ContentType` on every api-version); it accepts text, Office and HTML only. PDF is **batch-only** (`document/batches`), staging source and target in **blob containers via SAS**. So the translation pass is inherently an async, storage-backed step (the `salli_func` Azure-Function precedent), not an inline call.
- **Storage-provisioning gap:** `clinicalrecord-translator` is the raw Azure Translator resource (S1, uksouth) in the Azure DevTest subscription, resource group `AI_Shared_Dev`, which has **no storage account**, and Rowan **cannot create one** there. The only reachable staging account in that subscription is `stgsalli3odev` (Salli's dev storage, uksouth), where Rowan has data-plane and key access.

Paused 2026-07-10 on Rowan's decision of where to stage the PHI for the batch run. Related: [[project_medbrief-prod-file-access]], [[project_mri-134-branch]] (sibling workstream, same repo).
