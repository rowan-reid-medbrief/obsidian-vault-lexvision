---
date: 2026-07-04
project: /Users/Rowan.Reid/claude_code/medbrief
domain: medbrief
session: Fixed two MedBrief dev-environment blockers - a Mutagen root-owned-file permissions bug and a disabled-by-fixture-bug super-admin login
type: wrap-up
tags: [medbrief, mri-134, dev-environment, mutagen, permissions, security, login-bug]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief
    commit: dd0154a881f67e8cc8be001e591e51aefa2df50f
model_check: not-needed
---

## Session Summary

Diagnosed and fixed a `LoaderLoadException` on the dev VM caused by Mutagen syncing files as root-owned `0600`/`0700`: chmod'd the immediate offender plus the branch's other touched files, then made it permanent by recreating the Mutagen sync session with `permissions-mode=manual` (`0644`/`0755` on the VM side) while excluding `.env*` from sync to avoid loosening secrets. Separately diagnosed a login failure showing "Invalid credentials" as actually a disabled super-admin account (`UserFixtures.php`'s `USER_SUPER_ADMIN` fixture is missing `->setEnabled(true)`, unlike its siblings); confirmed via a throwaway password-encoder check that the password was correct, then fixed the account directly in the dev DB. Rowan declined the underlying fixture-code fix. Both issues and their workarounds are recorded in project memory for recurrence.
