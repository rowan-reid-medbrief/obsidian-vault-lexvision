---
date: 2026-06-16
domain: lexvision
tags: [meeting-pipeline, graph-to-insight, vault-hygiene, project-notes, calibration, gate2, domain-leak, cleanup]
repos: [ObsidianVault]
parent:
model_check: not-needed
---

# Discard the superseded meeting-pipeline re-apply; keep the project-note scaffolds

Reviewed the uncommitted output of the 12-13 June meeting-ingestion (graph-to-insight) re-apply on this Lexvision laptop. Since that pipeline work has moved to the Huble machine, discarded it as superseded: removed the nine pure-pipeline files (five per-meeting notes, two Reference Indexes, `Decisions/LOG.md`, `Areas/Shared - Active Commitments.md`) and stripped the machine-appended meeting sections from the two project hub notes, keeping only the hand-authored identity scaffolds. Net kept: created `Projects/lexvision/LexVision POC.md` (so `lexvision-poc` finally resolves via `reconcile.resolve_project_note`) and added `project_key` to the pre-existing `MedBrief Onboarding.md`; committed `83f05ca` (2 files, 11 insertions) and rebuilt the vault_index clean (no orphans/missing).

Earlier in the session: answered, from the calibration transcript, the Huble-roadmap question of whether the R6/H replay and GATE-2 numbers predate the `domain=None` leak. They do not: the leak was predicted at `/harden-plan` time and confirmed empirically during seeding on 12 June (~19:37), while the numbers were computed the next morning (13 June ~09:07), so the GATE-2 100% false-positive figure is leak-aware but uncorrected. Also ran read-only diagnostics (harvest replay metrics, store project_key/domain, Projects/ note scan) and proved the routing gate: claim/topic units land on the project hub note, while the other six unit types route by design to per-meeting/central notes via the crude M1 adapter.

**Where we left off / next:** the proper `/graph-to-notes` fold of the two MedBrief walkthrough graphs is still pending (the M1 `apply_insight` re-apply path mis-routes by unit_type and was discarded here); the meeting-pipeline build continues as the Huble programme. The `Projects/Lexvision` vs `Projects/lexvision` casing inconsistency is Rowan's to fix separately (now moot here: the only remaining file is the lowercase-resolved hub note).
