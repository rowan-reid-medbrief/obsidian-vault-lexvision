---
date: 2026-06-04
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Consolidated the 3 legacy expert-sheet outputs into one canonical experts_working.xlsx and repointed all phase script defaults at it
type: wrap-up
tags: [expert-sheet, medbrief, data-pipeline, combine-outputs, openpyxl]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: effe70a4ca7f3f679e1082dbcca6405cc5b391e3
---

## Session Summary

Summarised the five project workbooks, then tackled the real task: the three legacy outputs
(classified, with_profiles, deduped) were built by pre-partition scripts, so Phase 1.5's profile
block and Phase 2's dedup block both landed at column 22 and physically collide. Wrote a new
heavily-commented one-off `scripts/combine_outputs.py` that reconciles them into the current
3-block layout (classify P–U, dedup V–Z, profiles AA–BF): it takes the deduped file as the base
(already correct for A–Z), copies the profile block from cols 22–53 to 27–58 (a +5 shift past
V–Z), and guards on row-count + id-column alignment before writing. Verified the result
(`experts_working.xlsx`) against all three sources: 58 cols × 17,780 rows, base A–U byte-identical
to Output 1, dedup V–Z identical to Output 3, profiles AA–BF identical to Output 2's old block,
no collision residue, spot-check row carrying both a dedup match and a profile lands correctly.

Renamed the combined file to the canonical `data/outputs/experts_working.xlsx` (the name the code
comments already anticipated) and repointed all three phase scripts' default `WORKING_FILE`/
`INPUT_FILE` at it, so re-running any phase in `OUTPUT_MODE=overwrite` only touches its own block.
Committed on a branch, then merged fast-forward to `main` per Rowan's request to work only on
`main` in this project (saved as a feedback memory; overrides the global branch-first rule).
Next step for a future session: Rowan verifies the working file, then deletes the three legacy
outputs. Note `*.xlsx` is gitignored, so the working file lives on disk only, not in git.
