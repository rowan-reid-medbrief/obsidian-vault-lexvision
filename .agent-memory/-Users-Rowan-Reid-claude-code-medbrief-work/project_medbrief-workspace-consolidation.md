---
name: medbrief-workspace-consolidation
description: MedBrief Claude Code work is consolidated into one medbrief-work workspace nesting the product checkout as repo/
metadata: 
  node_type: memory
  type: project
  originSessionId: 0e6516bd-6075-4c5e-9c1e-13f5dea3fe81
---

MedBrief Claude Code work is consolidated into a single vault-coupled workspace `~/claude_code/medbrief-work` (the former apprise-viewer-rendering project, renamed) that nests the live GitHub product checkout as a gitignored `repo/`. The `annotations` project is deliberately out of scope for good, because it does not run against a MedBrief checkout. Decided with Rowan 2026-07-09 after a full `/harden-plan` pass, and completed the same day (Stages 1-5, all proven).

Stray tracking files (IDEAS.md, MEMORY.md) can no longer land in the product repo: a machine-local guard was added to the checkout's `.git/info/exclude` (Stage 1, done 2026-07-09). The workspace's git tracks only its own notes; `repo/` stays an independent gitignored repo (never flatten its `.git`).

**Why:** removes the think-in-notes / edit-in-checkout context switch (friction 1) and stops tracking files leaking into the vendor product repo (friction 2, the reported bug).

**How to apply:** launch Claude at the workspace root, not inside `repo/`; reach the code via `repo/`; run product git/tests as `(cd repo && ...)`. The migration is complete; the full record, including the mutagen sync config and the Stage 5 proofs, is in the workspace's `docs/MIGRATION-STATE.md`. Repo facts in [[medbrief-repo-github-migration]].
