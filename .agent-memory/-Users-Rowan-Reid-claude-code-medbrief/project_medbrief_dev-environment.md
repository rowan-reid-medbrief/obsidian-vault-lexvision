---
name: medbrief-dev-environment-bridge
description: "How this project's local medbrief checkout bridges to the running DigitalOcean dev VM via Mutagen (avoids manual SSH for editing)"
metadata: 
  node_type: memory
  type: project
  originSessionId: 558c9501-5f64-4e14-8ad9-f1fe341a0b6b
---

This project directory (`~/claude_code/medbrief`) is a real git clone of `medbriefteam/medbrief` (Bitbucket), git identity `rowan.reid@medbrief.co.uk`.

It is live-synced via **Mutagen** (session name `medbrief`) to Rowan's own DigitalOcean dev VM, where the actual docker stack runs (`app`, `php`, `db`, `db_test`, `mailcatcher` — confirmed up continuously, 6+ weeks uptime as of 2026-07-03). The sync excludes `.git`, `vendor`, `node_modules`, `var`, `tmp`, `data`, `public/build`, `public/bundles`, `public/app`, `storybook-static` (~1.3GB of build artefacts/dependencies that don't need to cross the wire). See [[medbrief-dev-vm-access]] for connection details.

**Why:** Rowan wanted to edit MedBrief code with Claude Code locally without SSHing into the VM by hand for every edit. Mutagen was chosen over SSHFS (the VM's `vendor`/`node_modules` are 1.3GB — too slow over a real network filesystem) and over a plain git-clone-and-push cycle (loses live edit-and-see-it-running feedback). Edits made locally reflect on the VM within a couple of seconds; the running containers bind-mount the whole repo (`../:/var/www/html:delegated`) so no rebuild is needed.

**How to apply:** Because `.git` is excluded from sync, all git operations (branch, commit, push) should happen on this Mac side, not on the VM directly — the VM's own `.git` won't know about branches created here. Check sync health with `mutagen sync list`; pause/resume with `mutagen sync pause/resume medbrief`. Note: this Mac's Homebrew has tap-trust enabled, and the auto-mode classifier blocks Claude from running `brew trust` itself even with user approval — ask Rowan to run trust commands himself when a new tap is needed.
