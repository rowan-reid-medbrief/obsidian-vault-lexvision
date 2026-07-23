---
name: medbrief-tracked-secrets-egress
description: msr-medbrief has 7 sensitive files tracked in git (keys plus four .env); untrack-and-rotate is the only real control on Copilot read-mode egress
metadata: 
  node_type: memory
  type: project
  originSessionId: 602fca14-d0be-4d68-b01e-6eb29b7532ce
  modified: 2026-07-23T14:06:09.125Z
---

`git@github.com:medbrief/msr-medbrief.git` (checkout at `~/claude_code/medbrief-work/repo`) carries **seven sensitive files tracked in git**, so they are on the remote and in history: `docker/jwt/private.pem`, `docker/jwt/public.pem`, `docker/keys/xero-dev-privatekey.pem`, `.env`, `.env.dev`, `.env.test`, `sentry/.env`. `.env.local` is untracked (local-only). Measured live 2026-07-23 across 4,636 files.

**Why:** it matters beyond ordinary hygiene because the Copilot CLI has no scoped read-deny, so anything inside a repo a read-mode dispatch runs against is egressable and the wrapper can only disclose it, never prevent it. Untracking and rotating is therefore the *actual* control, not a compensating one. The plan that surfaced this recorded the `.env` files as untracked; they are tracked, so do not trust that earlier characterisation.

**How to apply:** before proposing any Copilot consult or review against this repo, expect the `reachable_sensitive_paths` warning and treat it as disclosure rather than reassurance. The remediation is filed `[high]` in `~/claude_code/medbrief-onboarding/docs/IDEAS.md` (2026-07-23), beside the 2026-06-23 storybook-static credential leak; both point at the same habit and are worth raising with Deon together, with a repo-wide sweep plus a pre-commit guard to close the class. `/gh-copilot preflight --repo <repo>` prints the current list.

Related: [[copilot-substrate-plan-r3]].
