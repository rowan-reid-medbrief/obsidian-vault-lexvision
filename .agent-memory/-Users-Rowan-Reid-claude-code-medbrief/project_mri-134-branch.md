---
name: medbrief-mri-134-branch
description: "Branch feature/MRI-134-page-subset-extraction tracks Deon's Apryse page-subset/date-range viewer research ask"
metadata: 
  node_type: memory
  type: project
  originSessionId: 558c9501-5f64-4e14-8ad9-f1fe341a0b6b
---

Branch `feature/MRI-134-page-subset-extraction` (off `develop`) in this checkout tracks Jira [MRI-134](https://medbrief.atlassian.net/browse/MRI-134) — "Date Filter | Filter documents within pdf's by date filter" (Story, High, In Progress). The ticket is assigned to Deon Kuhn (CTO) himself, not Rowan, but Deon asked Rowan directly to assist/take it forward (an informal ask from a 2026-07-01 catch-up; only formally ticketed as MRI-134 as confirmed 2026-07-03).

**Why:** the full research, discovery findings, and hardened implementation plan live in a separate, sibling Claude Code project: `~/claude_code/projects/apprise-viewer-rendering` (`docs/PLAN.md`, `docs/OVERVIEW.md`, `docs/DESIGN-NOTES.md`). This `medbrief` checkout is only the implementation target — Workstream A of that plan (a page-list extraction endpoint, reusing PDFNet tooling) gets built here.

**How to apply:** Before starting implementation, re-read `~/claude_code/projects/apprise-viewer-rendering/docs/PLAN.md` for current status/steps. Follow this repo's own `docs-ai-sdd/prompts/msr-task-priming.prompt.md` ritual before editing. Since the ticket is assigned to Deon, confirm reassignment (or at least visibility) with him/Chantel before opening a PR. See [[medbrief-dev-environment-bridge]] for the local/VM setup this branch runs against.
