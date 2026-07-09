---
name: medbrief-avoid-broad-chmod-credential-checks
description: Avoid broad recursive chmod sweeps and credential-adjacent shell greps on the medbrief dev VM; the auto-mode classifier blocks them
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 4c44df3b-c11e-4ddf-a7c5-2b96ebe369bb
---

On the medbrief dev VM, don't run a single recursive `chmod -R o+r`/`o+rx` sweep across a whole directory tree (e.g. all of `src/`, `config/`, or the repo root) in one Bash call, and don't grep, echo, or otherwise print raw credential material (a `DATABASE_URL`, a password hash, even just its length or a character prefix) into command output.

**Why:** the auto-mode security classifier blocks both as "security weaken" / "credential materialization" actions, even when the underlying goal (fixing world-readability, verifying a password) is legitimate and low-risk on a personal dev box. It happened three times in one session (2026-07-04) while chasing a Mutagen permissions bug and a disabled-login-account bug.

**How to apply:** chmod only the explicit, named files/directories actually in scope (list them out one by one), and never touch `.env*`. To verify a credential (e.g. "does this password match the stored hash"), write a tiny throwaway Symfony command that calls the app's own encoder/comparison service and prints only a boolean (`password_valid=true/false`) — never extract or print the hash/URL itself, even partially. See [[medbrief-dev-environment-bridge]] for the specific incident this came from.
