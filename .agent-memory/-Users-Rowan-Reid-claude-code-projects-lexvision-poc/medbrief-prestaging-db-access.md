---
name: medbrief-prestaging-db-access
description: How to reach the MedBrief pre-staging medbrief-live DB for schema/aggregate-only reads
metadata: 
  node_type: memory
  type: reference
  originSessionId: 22898c53-7f72-488b-a13a-291109d507bb
---

The MedBrief pre-staging `medbrief-live` database is reachable read-only for schema and aggregate work (no row values, no PII) via a jumpbox tunnel plus the expert-sheet project's credentials.

- Bring up the tunnel: `az ssh vm -g JUMHOSTS -n Jumphost -- -L 3310:msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com:3306` (forwards `127.0.0.1:3310`). Check it with `nc -z 127.0.0.1 3310`.
- Credentials live in `/Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing/.env`, the `DB_*` set (host `127.0.0.1`, port `3310`, db `medbrief-live`, a read-only `ro*` user). The `STAGING_*` and `PROD_*` sets are empty. Connect with that project's venv python (`venv/bin/python3`, has pymysql); load the creds from `.env` inside the script and never print them.
- A live DB read needs explicit user approval each time: the auto-mode classifier treats it as a production read against shared infra and will block until the user approves. Keep strictly to `INFORMATION_SCHEMA` / `SHOW` / `DESCRIBE` / `COUNT(*)`.
- Schema findings (captured 2026-06-10, `docs/kumulus/research/c3b-db-schema.md`): 290 tables; patient identity PII is in `matterrequestpatient` (name, nhsNumber, dateOfBirth, address), not the imaging-oriented `patient` table; the medico-legal opinion is structured in `clinicalsummary`. Related: [[kumulus-engagement]].
