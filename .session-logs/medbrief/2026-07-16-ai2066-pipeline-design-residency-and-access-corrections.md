---
date: 2026-07-16
project: /Users/Rowan.Reid/claude_code/medbrief-work
domain: medbrief
session: Designed the AI-2066 translation pipeline and corrected two load-bearing claims that had been steering it wrongly (UK residency, and a storage blocker that never existed)
type: wrap-up
tags: [ai-2066, medbrief, compre, azure, document-translation, residency, dpa, rbac, phi, pipeline-design, apryse, azure-files, blob-storage]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-work
    commit: 37664e57fee57d4a622721b5746f11bdbbdd7069
model_check: fired-upgrade (model)
---

## Session Summary

Picked up AI-2066 (Compre translation) and found two recorded claims wrong on checking, both load-bearing and both from checking one thing then stating the general case. The translator is UK-hosted but Azure processes Document Translation in France Central / West Europe, so "region confirmed UK" was false and the UK-at-rest to EU-processing transfer needs a DPA answer from Deon; and "Rowan cannot self-serve storage" was true only of Azure DevTest, when he holds subscription-root Contributor on MedBrief Secure Review and could have created the staging account himself all along, so the six-day pause was on a blocker that did not exist.

Designed the pipeline the batch-only constraint forces (Files-to-Blob bridge, two-phase submit/collect with a persisted job id, managed identity over SAS, ephemeral PHI staging with soft-delete off), and recorded the headline risk: Azure silently translates only the digital portions of mixed digital/scanned PDFs, which is exactly the shape medical records are, so the output is a plausible-looking artifact with untranslated content. Also separated which claims rest on Microsoft's docs (the blob requirement, verbatim in three pages) from which rest on Rowan's own test (the PDF refusal, stated nowhere by Microsoft), because they are not equally citable.

Left a drafted, unsent Teams message to Deon and Laura that reports the findings, states Rowan will create staging himself, and asks only the two things he cannot answer alone. The spike is now technically unblocked and waits on a governance answer, not a permission.
