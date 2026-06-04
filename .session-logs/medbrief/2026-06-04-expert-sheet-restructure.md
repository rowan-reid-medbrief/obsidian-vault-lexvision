---
date: 2026-06-04
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Output-mode flags, data cleanup, and full project restructure for the Expert Sheet pipeline
type: wrap-up
tags: [expert-sheet, medbrief, refactor, project-structure, output-mode, path-anchoring]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: f6d3ddb
---

## Session Summary

Continued the Expert Sheet data-processing work (Phases 1, 1.5, 2). Three pieces of work:

1. **Output-mode flags + column partition (commit `06cb9b5`).** Added a shared `OUTPUT_MODE`
   env flag (`newfile` default vs `overwrite` in place) and configurable `WORKING_FILE` input to
   all three pipeline scripts, with atomic temp-then-replace saves. Discovered the scripts'
   output columns collided (Phase 1.5 and Phase 2 both started at V), so partitioned them into
   non-overlapping blocks: Phase 1 P–U, Phase 2 V–Z, Phase 1.5 moved V→AA. This lets the scripts
   be re-run over one evolving file without clobbering each other.

2. **Data cleanup.** Deleted four superseded Phase-1 intermediate workbooks from `data/` (~6.6M),
   keeping only the authoritative `…152155.xlsx`, the deduped/with-profiles outputs, and the
   adjudication sample. Did this with explicit user confirmation (data/ is gitignored, so
   deletion is unrecoverable).

3. **Full project restructure (commits `6a58c07` + `f6d3ddb`).** Reorganised the flat root into
   `scripts/`, `data/{raw,interim,outputs}`, `docs/`, `deliverables/`, plus new `README.md` and
   `requirements.txt`; `reference_scripts/`, `.env`, `venv/` stay in root. The key constraint was
   8 hardcoded paths + `.env` loading, so every script now anchors paths to
   `PROJECT_ROOT = Path(__file__).resolve().parent.parent` and runs correctly from any directory.
   Tracked files moved with `git mv` (history preserved); honoured a precondition by waiting for
   Excel/Word files to be closed before moving them.

Verified throughout: all scripts byte-compile; Phase 2 and Phase 1.5 dry runs launched from
`/tmp` resolved the moved input with Column O recall 98% (proving path anchoring); overwrite-mode
writer smoke test confirmed P–U/V–Z/AA–BF land correctly with A–U preserved. Updated
`docs/DECISIONS.md` (D12–D16), `docs/PHASE2_STATUS.md` §9, and the three project memory files to
the new layout. Project work was done in Engineer mode; pipeline logic unchanged throughout.

**Outstanding (unchanged):** USE_DB deterministic pass → send Chantel the docx + classified xlsx →
confirm with Laura whether full profile generation is Rowan's scope (gates the held AI
adjudication); triage the 348 Phase-1 unknowns.
