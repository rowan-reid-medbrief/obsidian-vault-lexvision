---
name: mri133-db-access
description: "How to query the MedBrief pre-staging database (medbrief-live) for MRI-133 research, and where credentials live"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 62d479c6-b8dc-42c6-b2e0-b07d564b17c0
---

Read-only DB access for MedBrief data questions (annotation counts, sort-session data,
schema checks) goes through the Azure jumpbox tunnel documented in
`~/claude_code/projects/expert-sheet-data-processing/docs/DB_TUNNEL.md` (a different
project — that's just where the tunnel setup was first documented, 2026-06-09).

- Pre-staging (safe to query freely, read-only user): local port 3310 →
  `msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com`, db `medbrief-live`.
- Production also has a tunnel port (3308, internal IP `10.3.4.4`) — do not query production
  without explicit sign-off; prior sessions have deliberately restricted tooling to port 3310
  only.
- Open the tunnel: `az account set --subscription 7b66abb8-9aed-44ce-bc82-c5d07d6b9a93` then
  `az ssh vm -g JUMHOSTS -n Jumphost -- -L 3310:msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com:3306`.
  Check first with `lsof -iTCP:3310 -sTCP:LISTEN` — Rowan often already has it open.
- **Credentials for this project (annotations) live in this project's own `.env`**
  (gitignored, `DB_HOST`/`DB_PORT`/`DB_USER`/`DB_NAME`/`DB_PASSWORD`), added 2026-07-02
  specifically so DB research could happen inside this project without reaching into another
  project's secrets. No local `mysql` client or Python MySQL driver was preinstalled; a
  throwaway venv with `pymysql` in the scratchpad directory worked (system Python nor the
  poc venv had a driver).

**How to apply:** before touching credentials in a different, unrelated project (e.g. the
expert-sheet-data-processing `.env`), stop and ask — the permission system blocks that
pattern as credential-scanning, correctly. Use this project's own `.env` instead.
