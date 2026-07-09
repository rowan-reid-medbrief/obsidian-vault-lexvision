---
name: medbrief-workspace-consolidation
description: MedBrief Claude Code work is consolidating into one medbrief-work workspace nesting the product checkout
metadata: 
  node_type: memory
  type: project
  originSessionId: 0e6516bd-6075-4c5e-9c1e-13f5dea3fe81
---

MedBrief Claude Code work is consolidating into a single vault-coupled workspace `~/claude_code/medbrief-work` (this apprise-viewer-rendering project, renamed) that nests the live GitHub product checkout as a gitignored `repo/`. The `annotations` project is deliberately out of scope for good, because it does not run against a MedBrief checkout. Decided with Rowan 2026-07-09 after a full `/harden-plan` pass.

Stray tracking files (IDEAS.md, MEMORY.md) can no longer land in the product repo: a machine-local guard was added to the checkout's `.git/info/exclude` (Stage 1, done 2026-07-09). The workspace's git tracks only its own notes; `repo/` stays an independent gitignored repo (never flatten its `.git`).

**Why:** removes the think-in-notes / edit-in-checkout context switch (friction 1) and stops tracking files leaking into the vendor product repo (friction 2, the reported bug).

**How to apply:** launch Claude at the workspace root, not inside `repo/`; reach the code via `repo/`; run product git/tests as `(cd repo && ...)`. Live status and remaining stages are in the project's `docs/MIGRATION-STATE.md`. Repo facts in [[medbrief-repo-github-migration]].
