---
name: project-expert-sheet-data-processing
description: "Context for the Expert Sheet Data Processing project — goals, tasks, data, and infrastructure"
metadata: 
  node_type: memory
  type: project
  originSessionId: dc9c2b3e-d8c0-4581-ad1d-173ac014cbbf
---

## Project: Expert Sheet Data Processing

> **Folder structure (restructured 2026-06-04, commits 6a58c07 + f6d3ddb).** The flat root was
> reorganised: `scripts/` (classify_users, generate_profiles, detect_duplicates, generate_email_docx),
> `data/raw/` (master list), `data/interim/` (checkpoints, logs, dedup sample), `data/outputs/`
> (classified / deduped / with_profiles workbooks), `docs/` (DECISIONS.md, PHASE2_STATUS.md),
> `deliverables/` (Chantel docx), plus root `README.md` + `requirements.txt`. `reference_scripts/`,
> `.env`, `venv/` stay put. Every script anchors paths to repo root (`Path(__file__).parent.parent`),
> so run as `venv/bin/python3 scripts/<name>.py` from any dir. Decision: [[project-phase2-dedup]]
> D16 in `docs/DECISIONS.md`. Paths below are pre-restructure; map root scripts → `scripts/`, the
> classified/output xlsx → `data/outputs/`, the master → `data/raw/`.

> **Canonical working file (consolidated 2026-06-04, commit `effe70a`).** The three legacy
> outputs (`experts_classified_…152155`, `experts_with_profiles_…161909`, `experts_deduped_…084115`)
> were produced by pre-partition scripts, so Phase 1.5's profile block and Phase 2's dedup block
> both landed at col 22 and collided. New one-off `scripts/combine_outputs.py` reconciles them into
> `data/outputs/experts_working.xlsx` matching the current 3-block layout (classify P–U, dedup V–Z,
> profiles AA–BF): it takes the deduped file as base, copies the profile block 22–53 → 27–58 (+5
> shift), guards on row-count + id alignment. All three phase scripts now **default
> `WORKING_FILE`/`INPUT_FILE` to `experts_working.xlsx`**, so re-running any phase in
> `OUTPUT_MODE=overwrite` only touches its own block. Next step: Rowan verifies the working file,
> then deletes the three legacy Output 1/2/3 workbooks. (`*.xlsx` is gitignored — the working file
> is on disk only, not in git.)

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
   - **Phase 2 status (2026-06-02):** `detect_duplicates.py` built & validated (~98% recall vs Col O); full AI adjudication held — see [[project-phase2-dedup]] and `PHASE2_STATUS.md`

### Data file
- Original: `experts master list (for ai processing)_260526.xlsx` — shared in Teams channel
- Local copy: `data/raw/experts_master_list_260526.xlsx` (moved here in the 2026-06-04 restructure; was project root)
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

### classify_users.py (updated session 2026-06-01)
Main Phase 1 classification script — now at `scripts/classify_users.py` (was project root). Committed on `main`.
- Steps: DB enrichment → rule-based classification → Gemini AI (batched) → write new columns to spreadsheet
- Adaptability flags: `RULE_BASED_ONLY`, `DRY_RUN`, `MAX_AI_ROWS`, `CHECKPOINT_INTERVAL`, `BATCH_SIZE`
- Current flags (as committed): `DRY_RUN=False`, `MAX_AI_ROWS=None`, `RULE_BASED_ONLY=False`, `BATCH_SIZE=20`
- DB query split into 3 separate queries to avoid MySQL sort buffer overflow on large GROUP BY
- **Batching**: 20 rows per Gemini call. ~20x faster. Falls back to `unknown` per row on batch error.
- **Output format (updated 2026-06-01)**: Column L (Chantelle's existing user type) is NEVER modified. All script output goes to new columns P–U:
  - P: `classification source` (e.g. `rule: agency_email`, `AI: gemini-2.5-flash`)
  - Q: `our user type` (our classification)
  - R: `confidence` (high/medium/low; blank for rule-based)
  - S: `reasoning` (one sentence from Gemini, or plain-English rule description)
  - T: `db roles` (role keywords from fos_user.roles)
  - U: `db user type` (fos_user.userType field)
- `apply_rules` returns `dict` with user_type/source/confidence/reasoning (was just a string)
- Checkpoint backfill: old checkpoints missing source/db_roles/db_user_type are enriched from the DB step at load time

### Full run status (completed 2026-06-01)
- First pass output: `data/experts_classified_20260601_120322.xlsx` (gemini-2.5-flash)
- Second pass output: `data/experts_classified_20260601_121332.xlsx` (gemini-3.1-pro-preview retry on unknowns)
- Second pass resolved 175 of 427 unknowns; 252 remain
- Second pass distribution: medical expert 1,115 | law firm 964 | unknown 252 | non-medical expert 169 | expert agency 159 | case management 98 | pagination agency 39 | internal 12 | competitor 2

**Final clean run (2026-06-01, complete):**
- Output (authoritative Phase 1 file, input to Phase 1.5 & 2): `data/outputs/experts_classified_20260601_152155.xlsx`
- All 2,728 AI rows genuinely processed by `gemini-3.1-pro-preview`; source attribution correct throughout
- 20 rows failed mid-run due to Gemini API connection reset; retried separately and resolved (18 classified, 2 remain unknown)
- Final distribution: law firm 1,098 | medical expert 1,021 | unknown 348 | non-medical expert 101 | expert agency 136 | case management 69 | pagination agency 31 | internal 5 | competitor 1
- 348 unknowns are all genuinely ambiguous (no batch errors in count)
- Current script state: `GEMINI_MODEL = "gemini-3.1-pro-preview"`, `RETRY_UNKNOWNS = False`, `DRY_RUN = False`

### Laura's AI enrichment spreadsheet (identified 2026-06-01)
- File: `expert_data_collection_v2_07-25.xlsx`, sheet `experts_AI_prefilled (251010)`
- This is the raw input to `production_main.py` — Laura used `gemini_file.py` + Perplexity to research expert profiles from public sources (LinkedIn, NHS, etc.) and extract specialty, qualifications, experience, career history, job title, location, years of experience
- Columns include: Model (A), status (C: done/not_found/remove/skip_re), email (F), Direct Email (G), Title (H), expert type (I), Specialty (J), Sub-Specialties (K), Job Title (P), City (Q), Country (R), Years of Experience (S), Experience (T), Career History (U), Academic Posts (V), Qualifications (W)
- This is profile enrichment for already-confirmed experts — NOT the same task as Rowan's Phase 1 classification

### DB findings — role structure confirmed (2026-06-01)
- Roles are per-case: format is `ROLE_PROJECT_<case_id>_EXPERT` — so a user with 31 invitations has been on 31 cases
- 153,659 total expert/scanner role rows across 25,077 distinct users
- Also: `ROLE_EXPERTAGENCY_<id>_ADMINISTRATOR` for agency admin roles; `EXPERTVIEWER` is a separate role type

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
