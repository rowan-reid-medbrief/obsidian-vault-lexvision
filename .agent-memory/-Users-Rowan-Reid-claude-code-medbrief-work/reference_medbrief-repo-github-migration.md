---
name: medbrief-repo-github-migration
description: "MedBrief product repo moved from Bitbucket to GitHub (~late June 2026); GitHub is canonical, Bitbucket left behind"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 0e6516bd-6075-4c5e-9c1e-13f5dea3fe81
---

MedBrief migrated the product codebase from Bitbucket (`medbriefteam/medbrief`) to GitHub (`medbrief/msr-medbrief.git`) around late June 2026 (about two weeks before 2026-07-09). Same codebase; GitHub is now canonical and the Bitbucket repo is being left behind.

- Live local checkout: `~/claude_code/medbrief` (GitHub remote, was on branch `feature/MRI-134-pdf-split-approach`). This is the one nested into the workspace as `repo/` (see [[medbrief-workspace-consolidation]]).
- Stale copy: the Bitbucket clone at `~/claude_code/medbrief-onboarding/repos/secure-review/medbrief`. Older project docs (apprise `docs/SOURCES.md`) cite this Bitbucket clone for code line-references; those citations should be repointed to the GitHub checkout since it is the same codebase.
