---
name: db-research-access
description: "Read-only MedBrief pre-staging DB access for code-grounded research (creds location, ports, runner pattern, PHI rule)"
metadata: 
  node_type: memory
  type: project
  originSessionId: d3899182-3a75-4b96-9eeb-8071d4c4ba42
---

For code-grounded research in this project, the MedBrief MySQL is reachable read-only over an SSH jumpbox tunnel that Rowan brings up. Connection details (host/user/password/db) live in the sibling project's env file: `~/claude_code/projects/expert-sheet-data-processing/.env`.

Ports (all `127.0.0.1` via the tunnel): **3310 = pre-staging** (UK South, schema named `medbrief-live`, user `rowan.reid`), **3308 = production**, 3309 = staging (rowan.reid not provisioned there). Use pre-staging (3310); never point research at prod.

Reading the DB is **regular sanctioned work** (Rowan's words, 2026-06-18), done across this and the Expert Sheets project. Pattern that worked for the MRI-133 research: a throwaway PyMySQL venv plus a guarded runner that asserts the pre-staging port and refuses anything but `SELECT`/`SHOW`/`DESCRIBE`. Keep to aggregates, schema, and ids; do **not** put raw patient content into git-tracked notes or docx (pre-staging may hold a prod snapshot). No `mysql` client is installed locally, so PyMySQL is the route. The Expert Sheets project has a fuller tunnel runbook at its `docs/DB_TUNNEL.md`. See [[project_ado-primary-code-host]].
