---
name: project-expert-sheet-data-processing
description: "Context for the Expert Sheet Data Processing project — goals, tasks, data, and infrastructure"
metadata: 
  node_type: memory
  type: project
  originSessionId: dc9c2b3e-d8c0-4581-ad1d-173ac014cbbf
---

## Project: Expert Sheet Data Processing

Meeting held 27 May 2026, 12:30–12:52 (Teams channel: "Kick-off re Expert Sheet Data Processing").

### Goal
Process an Excel file of expert profiles using AI (Gemini) to:

1. **Classify user type** for each expert. Categories:
   - medical expert
   - law firm
   - clerk/barrister
   - expert agency
   - pagination agency
   - non-medical expert
   - case management agency
   - Column G (domain) is a useful signal for classification

2. **Detect duplicate users**. Current state:
   - Some duplicates already linked via Column A (`id`) — the id of one of the pair is referenced
   - Some duplicates flagged by Column C (count > 1) — but only exact name matches
   - Need to also catch: name with title prefix, initial only, name in email address, and other variations
   - Note: existing dupes in `fos_user` are **soft deleted** users

### Data file
- Original: `experts master list (for ai processing)_260526.xlsx` — shared in Teams channel
- Local copy: `/Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing/experts_master_list_260526.xlsx`
- Sheet name: `MASTER_260512`
- **17,778 data rows** (rows 3–17780; row 1 = headers, row 2 = sub-headers "invited"/"accepted" for cols J/K)
- Note: meeting mentioned ~29,000 — actual file is 17,778; Chantel may have pre-filtered

### Confirmed column structure (from Python/openpyxl analysis)
| Col | Header | Notes |
|-----|--------|-------|
| A | `id` | fos_user ID; also used to link duplicates in col O |
| B | `name` | Raw name from DB (may include titles, numbers) |
| C | `COUNT same name` | COUNTIF formula — name duplicate signal |
| D | `TEMP first name` | Cleaned first name |
| E | `TEMP last name` | Cleaned last name |
| F | `email` | |
| G | `COUNT same emails` | COUNTIF formula — email duplicate signal |
| H | `TEMP domain` | Email domain extracted |
| I | `last_login` | datetime or 'NULL' string |
| J | `expert+scanner user roles` | Invitation count (sub-header: "invited") |
| K | (no header) | Accepted count (sub-header: "accepted") |
| L | `user type` | **Main output column** — partially filled |
| M | `mm experts` | Medbrief Match expert ID if already added |
| N | `mm linked profiles` | Linked profile count in MM |
| O | `duplicate` | Linked duplicate fos_user ID |

### Spreadsheet current state (as of 27 May 2026)
**User type distribution:**
- `medical expert`: 12,385 (69.7%)
- `None` (unclassified): **2,810 (15.8%)** ← needs classifying
- `expert agency`: 2,506 (14.1%)
- `pagination agency`: 51 (0.3%)
- `case management`: 23 (0.1%)
- `competitor`: 2
- `expert?`: 1 (uncertain — needs resolving)

**Row colour coding (confirmed via openpyxl):**
- `00000000` (no fill): 15,661 rows — standard
- `FFEBF2E4` (light green): 1,888 rows — already in Medbrief Match
- `FFFFFBE6` (light yellow): 224 rows — linked duplicate profiles
- `FFFFFF00` (bright yellow): 3 rows — unknown, worth checking
- Duplicate column filled: 1,893 rows

**Categories from brief NOT yet seen in data** (likely in the 2,810 unclassified): `law firm`, `clerk/barrister`, `non-medical expert`

### Scripts (from Laura's email)
- `expert_match` repo: `rnd/expert_data_collection/gemini_file.py` — Gemini script for expert profile extraction
- `expert_match` repo: `rnd/data_cleaning/deduplicate_experts.ipynb` — deduplication notebook
- `utils` repo: `common_utils/helper_textprocessing.py` — field cleaning helpers (use by importing as Python package)
- `utils` repo docs: https://medbrief.atlassian.net/wiki/x/A4CQPg

### Infrastructure
- **Gemini API key**: Azure Key Vault `expertmarketplace-kv`, secret `GEMINI-API-KEY`
- **common_utils pip install URL**: Azure Key Vault `expertmarketplace-kv`, secret `PIP-URL`
- Laura granted Rowan access to `expertmarketplace-kv` on 27 May 2026
- GCP direct access not set up — using Azure Key Vault for API key only

**Installing common_utils — DONE (session 2026-05-28)**:
- `venv/` created at project root
- `~/.pip/pip.conf` configured globally with Azure Artifacts feed URL (retrieved `PIP-URL` from `expertmarketplace-kv`)
- `common_utils==0.2.1193` installed (Confluence doc references 0.1.2 which no longer exists on the feed; 0.2.1193 is the latest stable)
- Confluence docs: https://medbrief.atlassian.net/wiki/spaces/MD/pages/1049657347/ ("Azure artifact feed: common_utils package" by Fatima Rahman)
- Azure Artifacts feed: https://dev.azure.com/MedBrief/MedBrief%20AI/_artifacts/feed/ai-utils

**Useful common_utils functions for this task**:
- `helper_textprocessing.normalise_name` — strips titles (Dr, Prof, Mr etc.), parentheses, initials, extra spaces from raw names. Use before sending to Gemini (Phase 1) and before fuzzy matching (Phase 2).
- `helper_textprocessing.normalise_text` — handles NaN, "not available" strings, whitespace cleanup. Use to sanitise email/domain fields.
- `rapidfuzz` — installed as a dependency; the main library for fuzzy name matching in Phase 2 duplicate detection.

**Why:** Pre-existing Gemini script may have stale field definitions vs. current `fos_user` schema — always verify schema alignment before running.
**How to apply:** Before executing any Gemini extraction script, compare its field/enum definitions against the current database schema.

### Script issues identified (session 1)
**`gemini_file.py`** — for profile *collection* (web research), NOT classification. Issues:
- Model `gemini-3-pro-preview` is not a valid model name — needs updating
- Hardcoded to old input file `rnd/data/citied_judgements_experts_03-11-25.xlsx` / sheet `other_experts`
- `ExpertTypeEnum` only has 5 values; needs the 7 categories from brief
- Column names (`Email`, `Last Name`, `First Name`, `ID`) need verifying against new spreadsheet

**`deduplicate_experts.ipynb`** — resolves already-identified duplicate groups (uses Azure OpenAI, not Gemini). Does NOT detect new duplicates — assumes `dup_group_id` already populated. A fuzzy detection step is needed first.

**`helper_textprocessing.py`** — good utilities: `normalise_name` strips titles/initials/parens, specialty validation, field cleaning. `ALLOWED_TYPE = {'expert'}` is fine for profile DB but not for classification task.

### Reference scripts saved locally (committed to git)
All scripts in `/Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing/reference_scripts/`
- Git repo initialised; 2 commits on `main` (initial scripts + .gitignore; .vscode/ added to .gitignore)
- Ignored: `venv/`, `.env`, `*.xlsx`, `.vscode/`

### classify_users.py (updated session 2026-05-29)
Main Phase 1 classification script at project root. Committed on `main`.
- Steps: DB enrichment → rule-based classification → Gemini AI (batched) → write back to spreadsheet
- Adaptability flags: `RULE_BASED_ONLY`, `DRY_RUN`, `MAX_AI_ROWS`, `CHECKPOINT_INTERVAL`, `BATCH_SIZE`
- Current flags (as committed): `DRY_RUN=False`, `MAX_AI_ROWS=None`, `RULE_BASED_ONLY=False`, `BATCH_SIZE=20`
- DB query split into 3 separate queries to avoid MySQL sort buffer overflow on large GROUP BY
- **Batching**: 20 rows per Gemini call (was 1). ~20x faster. Falls back to `unknown` per row on batch error.

### Full run status (completed 2026-05-29 09:44)
- **COMPLETE** — output: `data/experts_classified_20260528_171319.xlsx`
- 2,810 rows written; 14,968 skipped (already classified)
- 4 batch errors (rows 1680–1699, 2200–2219, 2280–2299, 2320–2359 — connection resets); 0 rows lost
- Category distribution (newly classified rows):
  medical expert 1,034 | law firm 896 | unknown 427 | non-medical expert 158 | expert agency 153 | case management 95 | pagination agency 39 | internal 6 | competitor 2
- **Next**: review 427 unknowns — manual triage or second AI pass with tighter prompting

### DB findings (session 2026-05-28)
- `helper_sql.get_medbrief_db_sql_connection` hardcodes port 3308 for local env — CANNOT USE for pre-staging (3310). Use raw pymysql.
- `userinternal` table: 4 regex patterns (`@medbrief.com`, `.net`, `.co.uk`, `.dev`) for internal staff detection
- `userexpertagency` table: 47 email substrings for agency detection
- `fos_user.roles` is PHP-serialised — use `extract_php_serialized_values` from common_utils, not string `in` checks
- Azure Key Vault access works via DefaultAzureCredential (AzureCliCredential) — confirmed working

### Gemini API key status (as of 2026-05-29)
- New working key confirmed in Key Vault `expertmarketplace-kv` / `GEMINI-API-KEY` (verified 2026-05-29)
- Old blocked key (`AIzaSyBtpF8...`) has been replaced — no action needed
- Model: `gemini-2.5-flash` (`gemini-2.0-flash` returned 404 NOT_FOUND — no longer available to new users)
- Script fetches key from Key Vault at runtime via `helper_azurekeyvault.get_secret_from_key_vault`

### Spreadsheet context (from Chantel & Laura)
- Source: all `fos_user` rows with **expert** or **scanner** role types (~29,000 total rows)
- **Scanners are included** because some experts were mistakenly assigned the scanner role rather than expert
- Chantel also added a sub-query for users who *accepted* those role types (vs just invited)
- Purpose: populate Medbrief Match with expert profiles (specialty, etc.) so clients can browse experts per specialty

**Row colour coding in the spreadsheet:**
- 🟢 Green = expert already in the Medbrief Match expert database
- 🟡 Yellow = duplicate profile linked to a primary expert (already accounted for)
- Green + Yellow = already handled; everything else needs processing

**Previous Expert Match data collection process (Laura):**
- Previously: subset of experts run through AI to collect title, specialty, sub-specialties, job title, location, years of experience, summaries
- A team of clinicians verified the AI output before experts were added to Medbrief Match
- Data in production is *reliable but incomplete* — capacity constraints meant only a subset was processed
- Process was non-standardised (multiple spreadsheets, various queries)
- Initially required experts to have an assigned case — now moving away from that; will use profile data directly

**Two-phase task:**

Phase 1 — Classify user type. Want to keep only **medical experts**. Remove:
- Fee earners / solicitors
- Medbrief internal users
- Deleted/removed profiles (soft deleted — for now, exclude)
- Non-medical experts (barristers, architects for PI, etc.) — may be wanted later but exclude for now
- Expert agencies, pagination agencies, case management agencies, law firms (see categories in tasks section)

Phase 2 — Duplicate detection (see tasks section above)

### Database access

**SSH tunnel command** (opens all three ports simultaneously):
```
az ssh vm -g jumhosts -n jumphost -- -L 3309:msr-staging-db-mysql.mysql.database.azure.com:3306 -L 3308:10.3.4.4:3306 -L 3310:msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com:3306
```

| Local port | Target | Environment |
|-----------|--------|-------------|
| 3309 | msr-staging-db-mysql.mysql.database.azure.com | Staging |
| 3308 | 10.3.4.4 | **Production** |
| 3310 | msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com | **Pre-staging** (use this) |

**Pre-staging credentials** (Rowan's personal user, confirmed by Deon):
- Host: 127.0.0.1, Port: 3310, User: rowan.reid, DB: medbrief-live
- Password in project `.env`

**Notes:**
- Pre-staging was migrated uk-west → uk-south; uk-west is being decommissioned
- Production DB: same credentials as pre-staging but different port (3308), confirmed by Deon
- Shared service account also exists: user=medbrief (password in .env comment, now removed)
- `.env` file at project root holds all credentials (gitignored)
- Attendees: Chantel van Wyk, Laura Gongas, Deon Kuhn, Rowan Reid
- ~18 minutes of transcript (1:23–19:04) is missing — key detail about spreadsheet columns may be in that gap
