# Project memory index - medbrief-work (MedBrief workspace)

One line per memory. Content lives in the linked files, not here. Merged 2026-07-09 from the former apprise-viewer-rendering and medbrief-checkout slugs during the workspace consolidation.

## Workspace and repo
- [MedBrief workspace consolidation](project_medbrief-workspace-consolidation.md) — medbrief-work nests checkout as repo/; leak-guard live
- [MedBrief repo GitHub migration](reference_medbrief-repo-github-migration.md) — product repo moved Bitbucket → GitHub ~late June 2026; Bitbucket left behind

## Dev environment
- [MedBrief dev environment bridge](project_medbrief_dev-environment.md) — Mutagen-synced local clone (now repo/) ↔ DigitalOcean VM, avoids manual SSH
- [MedBrief dev VM access](reference_medbrief_vm-access.md) — SSH/ZeroTier details for rowan-dev.medbrief.net
- [MRI-134 branch context](project_mri-134-branch.md) — both MRI-134 sibling branches (XOD page-subset + PDF split); full plan in this workspace

## Working feedback
- [Don't offer committing](feedback_no-offering-commits.md) — never propose/list committing; wait for an explicit request
- [Avoid broad chmod/credential checks](feedback_avoid-broad-chmod-credential-checks.md) — chmod named files only, verify passwords via app-level boolean checks, never dump credential material
- [Code-walkthrough audio: name files](feedback_code-walkthrough-audio-naming.md) — narrate files by name AND ordinal, not ordinal-only, when rendering a spoken code walkthrough
- [Code comment tone review](feedback_code-comment-tone-review.md) — check word choice against writing-voice.md, not just structural AI-tells
