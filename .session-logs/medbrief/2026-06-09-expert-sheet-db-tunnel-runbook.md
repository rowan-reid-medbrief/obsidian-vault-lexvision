---
tags: [expert-sheet, database-access, azure, jumpbox, ssh-tunnel, runbook, medbrief]
repos:
  - expert-sheet-data-processing (docs/DB_TUNNEL.md)
---

# Expert Sheet — DB tunnel / jumpbox runbook captured

Recovered the working Azure jumpbox SSH-tunnel command for Medbrief DB access from `~/.zsh_history` (one `az ssh vm` call against VM `Jumphost` / RG `JUMHOSTS` / subscription `MedBrief Secure Review`, forwarding pre-staging 3310, production 3308, staging 3309); it had survived only as a truncated comment in `scripts/classify_users.py`. Diagnosed the `Not Found` error as a subscription-context issue rather than a missing resource: `az ssh vm` does not reliably thread `--subscription` through its ARM calls, so it hits the default Azure DevTest subscription, and the fix is to run `az account set --subscription 7b66abb8-...` first. Stored it in a new `docs/DB_TUNNEL.md` runbook and refreshed the `project_expert_sheet.md` memory Database access section (corrected from the stale lowercase form); confirmed `.env` stays gitignored so nothing secret is exposed.
