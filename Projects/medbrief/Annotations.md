---
title: Annotations
domain: medbrief
created: 2026-06-19
tags: [mri-133, annotations, medbrief]
status: discovery
project_repo: "~/claude_code/projects/annotations"
project_key: "annotations"
---

# Annotations

Dedicated home for **MRI-133 "Granular storing of pages"**: keeping page-level work (annotations, redactions, solicitor references, AI-generated outputs) attached to the right underlying records when already-sorted medical records are updated or repaginated. The name "Annotations" is a convenience handle; the scope is broader, and the research reframes the problem as **rebinding references to the stable `Page.id` and recording page lineage**, not inventing an identity. ([MRI-133](https://medbrief.atlassian.net/browse/MRI-133))

## Status

**Discovery.** [[Deon Kuhn]] (CTO) asked [[Rowan Reid]] to take MRI-133 forward with further research and a proof-of-concept. The ticket is High, under epic MRI-89 "Data", reporter Chantel van Wyk, assigned to Rowan, status **Blocked / On Hold** (as of 2026-06-19). Research migrated out of [[MedBrief Onboarding]]; PoC not yet started.

## Relationship to MedBrief Data Strategy

This is the page-level lineage / annotations track under epic MRI-89 "Data". The company-wide data initiative lives in [[MedBrief Data Strategy]]; this project owns MRI-133 implementation detail, not the broader strategy.

## Detailed working project

Working detail for this initiative lives in the Claude Code project at `~/claude_code/projects/annotations` (the `project_repo` field above). That project owns the working detail; this note holds the hub layer. Per-topic detail:

- `docs/OVERVIEW.md` - start here: what it is, status, document map.
- `docs/SOURCES.md` - provenance and up-link map back to this note.
- `docs/DESIGN-NOTES.md` - project-tactical design notes (not a vault decision mirror).
- `docs/IDEAS.md` - project backlog.

## Decisions referencing this note

- [[2026-06-19-mri133-scope-and-stamp-first]]: scoped the POC to page-less documents (standalone Python, forward redaction-survival) and adopted stamp-first identity with content-matching as the fallback.
