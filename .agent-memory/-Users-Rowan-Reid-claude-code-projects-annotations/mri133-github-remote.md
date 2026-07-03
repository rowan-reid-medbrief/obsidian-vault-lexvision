---
name: mri133-github-remote
description: The annotations repo now has a private GitHub remote (set up 2026-07-03); how to push and the entire-hook quirk
metadata: 
  node_type: memory
  type: project
  originSessionId: 6710ab75-d68e-40b8-83c1-7b6ac6240a08
---

The `annotations` repo (MRI-133 PoC) has a **private GitHub remote** as of 2026-07-03. Before this there was no remote at all (the handoff loose end "push main, no destination yet").

- **Remote:** `origin` = `git@github.com:rowan-reid-medbrief/mri-133-annotations.git` (SSH), **private**.
- **Auth:** the SSH key `~/.ssh/github` authenticates as GitHub account **`rowan-reid-medbrief`** (a MedBrief account; wired as `Host github.com` in `~/.ssh/config`). Use SSH, not HTTPS: HTTPS could not authenticate non-interactively from the session.
- **`gh` CLI** was installed this session (via `brew`, v2.95.0) and authed as `rowan-reid-medbrief` (web-browser device login). Use it for repo/PR ops.
- **Default branch:** `main`.
- **Quirk — entire.io pushes its checkpoints branch too.** Every `git push` also triggers entire's pre-push hook to push `entire/checkpoints/v1` (session-capture checkpoints). Harmless (repo is private, secret scan was clean by filename), but expect it in push output. On the very first push it made the checkpoints branch the GitHub default; that was reset to `main` with `gh repo edit --default-branch main`.
- Before pushing a new branch: nothing sensitive is tracked (`.env` is untracked and was never committed; `poc/data/` is git-ignored, so real patient PDFs never reach the repo).
