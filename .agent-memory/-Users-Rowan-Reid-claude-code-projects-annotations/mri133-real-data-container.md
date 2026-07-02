---
name: mri133-real-data-container
description: Location and structure of the Azure Blob container Deon shared with real (non-synthetic) case documents for MRI-133 matcher testing
metadata: 
  node_type: memory
  type: reference
  originSessionId: a0fbe9f5-31f5-4dfb-96af-b87c042dafca
---

Deon gave access to a real-case-document source for trialling the MRI133 matching engine on non-synthetic data (per [[mri-133-project]] and the 2026-07-01 catch-up notes at `notes/catch-up-2026-07-01-meeting.md`).

**Location:** Azure Blob container `classify-document-http`, storage account `stgsalli3odev`, resource group `rg-salli3.0-dev`, subscription "MedBrief Secure Review" (`65483d0a-b13d-414b-a8e7-ec389e23dd84`).

**Access note:** Rowan has Owner (control-plane) on the storage account but no data-plane RBAC role (Storage Blob Data Reader/Contributor), so `az storage blob list`/`az storage blob download` with `--auth-mode login` fail. The Azure Portal blade falls back to access-key auth automatically (shows "Authentication method: Access key") since Rowan is Owner and can retrieve keys — browsing via the portal UI (claude-in-chrome) works; CLI data-plane access does not without either a data-plane role grant or manually-supplied key/SAS.

**Structure (surveyed 2026-07-01, metadata only, no file content opened):**
- `benchmarking-dataset/` — 30 files, `combined_XXXXXX.pdf`, single upload batch (16 Feb 2026), 6–155 MB. Looks like the clean, curated set — best starting candidate.
- `gp-records/` — 9 files, mixed naming (case-ID pairs, size variants, a `-test` file, plus later `combined_*` additions). Ad hoc/scratch, not clean.
- `salli-test/` — 5 files, case-ID named, 1.5 MB–972 MB. Real production-scale SALLI case bundles.
- `trust-records/` — 1 file, hash-named, 261 MB, looks auto-ingested via pipeline.

**Why this matters:** this is real patient data (GP/Trust medical records), not synthetic, and file sizes go up to ~1 GB — far beyond the 108-page synthetic corpus the matcher has been validated against. Before running the matcher at scale here, check actual page counts and confirm the data-handling boundary with Deon (can files leave Azure onto local disk, or must processing stay inside the existing perimeter).

**How to apply:** when picking up real-data testing for MRI133, start with `benchmarking-dataset`, and treat the other three folders as unvetted scratch data until confirmed otherwise.
