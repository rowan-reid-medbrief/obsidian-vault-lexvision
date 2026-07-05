---
name: mri133-background-cleanup-caution
description: "Before deleting a scratch/work directory in this project, check for a still-running background task that might be using it - this project routinely runs long background bake-off/safety-gate scripts."
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 89f771d0-ae72-4a4e-8945-9ffc03d75c8a
---

Mid-session (2026-07-05) an `rm -rf` on a scratch working directory (`poc/data/_diag_work`) killed
a still-running background diagnostic script that was writing into it, wasting the run. The
project routinely launches long (20-90 min) background bake-off/safety-gate scripts with their
own working directories under `poc/data/`.

**Why:** a careless cleanup command doesn't just fail loudly - it silently corrupts a still-running
process's output, and the failure only surfaces later as a confusing crash traceback.

**How to apply:** before any `rm -rf` targeting a `poc/data/` working directory, check for
in-flight background tasks (this session's own launched-in-background commands, or the OS process
list) first. Prefer cleaning up only paths under the session scratchpad, never a `poc/data/*_work`/
`*_gate`/`*_diag*` path a background run might still hold open.
