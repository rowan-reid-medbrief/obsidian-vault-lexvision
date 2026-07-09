---
date: 2026-07-09
project: /Users/Rowan.Reid/claude_code/medbrief-work
domain: medbrief
session: Ran Stages 2-5 of the MedBrief workspace consolidation - renamed the project to medbrief-work, nested the product checkout as repo/, recreated the mutagen sync, and repointed memory and vault pointers
type: wrap-up
tags: [medbrief, workspace-setup, project-structure, git, mutagen, memory, migration, mri-134]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-work
    commit: d575161
  - path: /Users/Rowan.Reid/.claude
    commit: 51a4dca
model_check: not-needed
---

## Session Summary

Ran Stages 2-5 of the MedBrief workspace consolidation from a neutral cwd: renamed `apprise-viewer-rendering` to `medbrief-work`, moved the msr-medbrief checkout in as a gitignored `repo/`, terminated and recreated the mutagen sync on the new alpha path (config verified against the saved spec, back to "watching"), merged both memory slugs under the workspace slug in the `~/.claude` store and the vault mirror, and repointed the vault hub note plus `docs/SOURCES.md`. A pre-flight `lsof` sweep caught a live Claude session rooted inside the very folder Stage 2 was about to rename, so the move was gated until it closed: the plan had given Stage 3 assertable checks but left Stage 2 a prose-only gate, and the calmer-looking stage carried the real risk.

All Stage 5 proofs passed (workspace and `repo/` are distinct git roots, the stray-file guard hides `repo/MEMORY.md` and `repo/docs/IDEAS.md`, `repo/` reaches msr-medbrief clean, mutagen reconnected, both vault pointers resolve). Two reflected learnings were logged centrally (#mp68ra assertable preconditions per migration stage, #muu70z grep relocated memory bodies for hardcoded paths), plus #1nengx for a `/log-idea` path-race found in skill reflection. The workspace's own note edits (`.gitignore`, `CLAUDE.md`, `docs/MIGRATION-STATE.md`, `docs/SOURCES.md`) and the vault hub note were deliberately left uncommitted: a concurrent agent was working that tree at wrap-up time, and had already split the workspace into per-ticket `docs/mri-134/` subdirs and resolved the hub note's `project_key` to `medbrief-work` (the follow-up this session had parked). Those commits belong to that session, not this one.
