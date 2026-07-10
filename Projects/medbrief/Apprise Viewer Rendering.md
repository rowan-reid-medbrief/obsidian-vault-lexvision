---
title: "Apprise Viewer Rendering"
domain: medbrief
created: "2026-07-01"
tags: []
status: in-progress
project_repo: "~/claude_code/medbrief-work"
project_key: "medbrief-work"
---

# Apprise Viewer Rendering

Hub note for the `medbrief-work` workspace: MedBrief product work on the Apryse (viewer) side, one ticket per subdir. Current ticket is MRI-134 (date-range page-filtering in the Apryse document viewer).

## Status

MRI-134: page-list extraction proven end-to-end (server-side PDF extraction and a XOD OPC-surgery subsetter both built and demoed live in the real Apryse WebViewer, 2026-07-04). Remaining before productionisation: Workstream B (the ChronologyItem Bates-page mapping needed for real date-range filtering) and cleanup (PII cache TTL, `Annots.xfdf` page-index remap). See `docs/mri-134/DESIGN-NOTES.md` for the full build log.

## Detailed working project

Working detail lives in the Claude Code workspace at `~/claude_code/medbrief-work` (the `project_repo` field above). That workspace owns the working detail; this note holds the hub layer. The workspace holds one subdir per ticket under `docs/`:

- `docs/SOURCES.md` - workspace-level up-link map back to this note, and the index of active ticket subdirs.
- `docs/IDEAS.md` - cross-ticket backlog.
- `docs/mri-134/OVERVIEW.md` - MRI-134: start here (what it is, status, document map).
- `docs/mri-134/PLAN.md` - MRI-134: the hardened build plan.
- `docs/mri-134/DESIGN-NOTES.md` - MRI-134: project-tactical design notes and the build log (not a vault decision mirror).
- `docs/mri-134/IDEAS.md` - MRI-134: ticket-scoped backlog.
- `docs/mri-134/SOURCES.md` - MRI-134: ticket-specific provenance (Jira ticket, codebase evidence, fixtures).
