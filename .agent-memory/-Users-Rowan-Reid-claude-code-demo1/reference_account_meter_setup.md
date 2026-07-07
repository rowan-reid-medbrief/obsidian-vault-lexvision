---
name: account-meter-setup
description: "How this laptop's multi-account \"shared brain, separate meter\" split routes cost between medbrief (primary) and personal via .claude-account"
metadata: 
  node_type: memory
  type: reference
  originSessionId: e63e53a0-d087-48c8-bf99-6154c03a2f57
---

This laptop runs medbrief as the machine primary (`~/.claude-primary`), with `~/.claude-personal` as an alt config dir for personal work. A project directory meters to the primary (medbrief) by default; it only meters to personal when its git root (or project root, if it isn't a git repo) contains a `.claude-account` file whose content is the literal string `personal`.

**Why:** Rowan wants medbrief work billed to the primary account and personal projects billed separately, without maintaining two full checkouts of every repo.

**How to apply:** Never write `medbrief` into a `.claude-account` file — untagged already resolves to medbrief, and an explicit `medbrief` tag would fail to resolve on another laptop where `medbrief` isn't a configured alt dir. When classifying a project's meter, check `git remote get-url origin` first; if ambiguous (no remote, or an unclear name), ask rather than guess. `~/claude_code/demo1` is tagged personal (as of 2026-07-07); the other repos under `~/claude_code` (and `~/claude_code/projects`) all resolved medbrief.
