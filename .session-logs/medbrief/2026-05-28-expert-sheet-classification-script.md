---
date: 2026-05-28
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Expert sheet Phase 1 — DB exploration, classification plan, classify_users.py
type: handoff

parent: 2026-05-28-expert-sheet-env-setup.md
---

## Summary

Built the Phase 1 classification script for the expert sheet project. Explored the medbrief-live DB schema (pre-staging) to find deterministic classification signals, audited all reference scripts and common_utils modules for reuse, wrote and tested classify_users.py.

## What was done

- Confirmed actual Column L values in spreadsheet vs. brief categories (discrepancies: `case management` not `case management agency`; `competitor` exists but not in brief)
- Full DB schema exploration: 290 tables, identified `userinternal` (4 patterns), `userexpertagency` (47 substrings), `fos_user.roles` (PHP-serialised) as key classification signals
- Cross-referenced 2,810 unclassified rows against DB signals: 82 deterministic (54 agency, 28 law firm), 2,728 need AI
- Audited all 17 common_utils modules — documented usage decisions for each
- Deep review of all 5 reference scripts — documented what to use, what not to, and why Laura sent each
- Built classification plan (saved to `~/.claude/plans/`)
- Created `classify_users.py` (heavily commented, with adaptability flags)
- Tested in dry-run / rule-based-only mode: pipeline runs end-to-end correctly
- Confirmed Gemini API key blocked (403); same key in both .env and Key Vault

## Open questions / blockers

- **Gemini key**: blocked. Laura needs to generate a new one at ai.studio/api-keys and upload to Key Vault: `az keyvault secret set --vault-name expertmarketplace-kv --name GEMINI-API-KEY --value "<new-key>"`
- **Canonical category strings**: needs Chantel confirmation before AI full run (esp. `case management` vs `case management agency`, `competitor` as output, `law firm` vs `clerk/barrister`)
- **18-min transcript gap**: key meeting detail may be in the missing 1:23–19:04 section; Rowan plans to re-watch recording

## State

- `classify_users.py` committed to main (commit 65b880f)
- DB tunnel: pre-staging port 3310 (needs `az ssh vm` tunnel running)
- `DRY_RUN=True`, `RULE_BASED_ONLY=True` in script — safe to run anytime
- To run AI step: update Key Vault key, set `RULE_BASED_ONLY=False`, `DRY_RUN=False`, keep `MAX_AI_ROWS=50` for first test batch

---

## Continuation Prompt

## Continuation: Expert Sheet Phase 1 — Ready for AI run

**Parent session:** 2026-05-28-expert-sheet-classification-script.md

### Context
Medbrief expert sheet project: classifying 17,778 `fos_user` rows (from `experts_master_list_260526.xlsx`) into user type categories so medical experts can be identified and loaded into Medbrief Match. Phase 1 is classification; Phase 2 is deduplication.

### What was done last session
- Explored medbrief-live DB schema (pre-staging, port 3310) — found `userinternal`, `userexpertagency`, and `fos_user.roles` as deterministic classification signals
- Audited all 5 reference scripts (shared by Laura) and all 17 common_utils modules — usage decisions documented inline in the script
- Built and committed `classify_users.py`: rule-based pre-classification → Gemini AI → write-back to spreadsheet
- Tested dry-run / rule-based-only: 82 rows classified deterministically (54 agency, 28 law firm), 2,728 queued for AI
- Confirmed Gemini API key is blocked (403 PERMISSION_DENIED) — same key in both `.env` and Key Vault

### Current state
- `classify_users.py` committed on `main` (commit `65b880f`) — script is ready, blocked on Gemini key
- `DRY_RUN = True`, `RULE_BASED_ONLY = True` in the script — safe defaults
- DB tunnel: `az ssh vm -g jumhosts -n jumphost -- -N -L 3310:msr-pre-staging-db-mysql--uk-south.mysql.database.azure.com:3306` (needs to be running for any DB step)

### Where we left off
Waiting on a new Gemini API key. Once Laura provides one, it goes into Key Vault and the AI step can run.

### Next steps
1. **Get new Gemini key from Laura** — generate at https://ai.studio/api-keys, upload with: `az keyvault secret set --vault-name expertmarketplace-kv --name GEMINI-API-KEY --value "<new-key>"`
2. **Confirm canonical category strings with Chantel** — esp. `case management` vs `case management agency`; whether `competitor` is a valid AI output; `law firm` vs `clerk/barrister`
3. **Re-watch meeting recording** — 18 min of transcript (1:23–19:04) is missing; may contain key details about expected output
4. **Test AI step**: set `MAX_AI_ROWS = 50`, `RULE_BASED_ONLY = False`, `DRY_RUN = True` → review 50-row sample before full run
5. **Full run**: set `DRY_RUN = False`, `MAX_AI_ROWS = None`

### Key references
- Script: `classify_users.py` (project root)
- Spreadsheet: `experts_master_list_260526.xlsx`, sheet `MASTER_260512`
- Key Vault: `expertmarketplace-kv`, secret `GEMINI-API-KEY`
- DB tunnel port: 3310 (pre-staging), credentials in `.env`
- Plan file: `~/.claude/plans/these-7-options-don-t-velvety-hartmanis.md`
- People: Chantel van Wyk (spreadsheet owner), Laura Gongas (reference scripts / Gemini key)
