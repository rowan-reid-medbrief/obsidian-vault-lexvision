---
tags: [medbrief, ai-2066, mri-134, azure, storage, infrastructure, confluence, jumphost]
repos:
  - medbrief-work
model_check: not-needed
---

# MedBrief storage architecture + production file access

Answered "how are MedBrief documents stored" definitively and confirmed Deon's claim that "only XOD is in blobs": the document representations (native, optimised PDF, OCR, page images) live on **Azure Files** SMB shares (account `msrstandard`, mounted as local paths, so the flysystem `local:` adapters read them), and **only XOD** is in Azure Blob (`xod_blob_fs`). Verified against the live subscription with `az` (management plane works; the data plane is firewalled from the laptop). Corrected the MRI-134 scale-test premise (the extraction source is Azure Files, not Blob) across `PLAN.md`/`OVERVIEW.md`, closed its open "Azure or local disk?" question, wrote `docs/storage-architecture.md` (three access routes plus the Confluence links), and indexed it in `SOURCES.md`.

Then stood up Rowan's production file access end to end: found the jumphost NSG (`Jumphost-nic-nsg`) was silently dropping his SSH because his IP had no allow rule, added the `RowanHome` rule (priority 1080), and confirmed the connection works (so he is also in `Infra_VM_login_user`). Derived the live-system URL scheme from the routing (`ssl.medbrief.co.uk/matter/{id}/documents/{docId}/stream-native/`) and handed over a PII-minimised SQL lookup; Rowan then downloaded the AI-2066 translation sample (case 44240 / doc 107785104) through the app UI. Saved a `project_medbrief-prod-file-access` memory.
