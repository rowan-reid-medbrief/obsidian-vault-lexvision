---
name: mri-133-project
description: "The dedicated home for Medbrief ticket MRI-133 (granular storing of pages), spun out of medbrief-onboarding."
metadata: 
  node_type: memory
  type: project
  originSessionId: a971cb17-2a08-4748-9281-d0f559e27622
---

This project (`~/claude_code/projects/annotations`, dir name "Annotations") is the dedicated home for Medbrief Jira ticket **MRI-133 "Granular storing of pages"**: keeping page-level edits (annotations, redactions, references, AI-generated outputs) attached when already-sorted records are updated or repaginated. The research reframes it as **rebinding references to the stable `Page.id` plus recording page lineage**, not inventing an identity (kernel: a reference names stable content; position lives in a separate `placement` table; a re-sort writes only placements).

**Provenance:** spun out of the `medbrief-onboarding` project on 2026-06-19. The bulk research (notes 14/15, the branded docx) moved into `docs/research/` and `output/`; onboarding keeps pointer stubs. Vault-coupled to `Projects/medbrief/Annotations.md`.

**Who / status:** Deon Kuhn (CTO) asked Rowan to take MRI-133 forward with further research and a proof-of-concept. Ticket is High, epic MRI-89 "Data", assigned to Rowan, status **Blocked / On Hold**. The PoC is intended to live in `poc/` inside this project; Deon owns the eventual MSR build.

**Boundary:** distinct from the two other medbrief hub projects, `medbrief-onboarding` (general developer onboarding) and `data_strategy` (company-wide data strategy). This project owns MRI-133 implementation detail only.

Start at `docs/OVERVIEW.md`; the substance is in `docs/research/`.
