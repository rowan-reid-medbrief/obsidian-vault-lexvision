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

**Update 2026-07-03 — corpus expanded to 11 real docs, downloaded locally.** Now **11** raw real docs in `poc/data/real-samples/` (git-ignored, PII stays out of the repo), up from the original 3. Rowan downloaded them via the Azure Portal (Owner → access-key auth); `az` CLI is installed + logged in at control-plane but has no data-plane role, so portal (or a manually-supplied key) is the download path. All **four provenances** now represented: benchmarking-dataset ×7 (`combined_108815/100200/115131/115132/115917/118830/118933`), gp-records ×1 (`126998-10606-test`), salli-test ×2 (`144017-12303` digital 32pp, `142257-12147` image-only 342pp), trust-records ×1 (`691c7696…` **1344pp digital unpaginated**). Spread confirmed by a text/pagination probe: full-digital → mixed → **three real image-only/no-OCR docs** (100200, 115132, 142257 — the scanned population is no longer synthetic-only; bench-115132, the twin case, is also image-only), and a strong **unpaginated** set (the dormant REMOVED-rule target). NB the image-only docs need the render-based ID path when stamped (no text layer). Next: stamp all into `_stamped/*.clean.pdf` + wire `scripts/real_bakeoff.py` to source all 11 (see [[mri133-cardinality-channels]] enable-gate).

**Correction 2026-07-05 — bench-115132 is NOT image-only.** A fresh, careful text-extraction check
(`poc/scripts/content_ceiling.py`) shows bench-115132 has real digital text: 172pp, only 50 blank,
61 distinct non-blank texts (122 pages are exact duplicates of one of those 61) - a repetitive
TEMPLATE doc, not an image-only one. The 2026-07-03 "three real image-only docs" classification
above was wrong for this doc; only **bench-100200** and **salli-142257** are genuinely 100%
image-only (no digital text layer at all).
