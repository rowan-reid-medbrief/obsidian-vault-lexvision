---
name: no-offering-commits
description: "Do not offer, suggest, or list committing as a next step; wait for an explicit request"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: cf4a6d5e-d7e5-4f65-b149-8a3c6eb7e051
---

Rowan does not want me to offer, suggest, or include "commit" in recommendations, next-step lists, or option menus. Wait for him to explicitly request a commit.

**Why:** He controls when work is committed. This is stronger than the default "commit only when asked" rule: he does not even want committing surfaced as an option. It reads as unwanted friction.

**How to apply:** Never propose committing, never put it in a recommended sequence or an AskUserQuestion option set, never say "want me to commit?". Only commit, or mention committing, once he asks. Do the verified work, leave it uncommitted, and stay silent about committing until prompted.

**Explicitly includes `/wrap-up` and similar end-of-session skills.** Their default flow commits uncommitted work as one of its steps; on this project (and generally, absent an explicit ask), skip that step and leave the working tree uncommitted. Reconfirmed 2026-07-04 on the MRI-134 branch, which by standing convention (see [[medbrief-mri-134-branch]]) stays uncommitted entirely, including a temporary dev-only Azure fallback marked for revert before any commit.
