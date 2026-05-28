---
date: 2026-04-23
project: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
session: Fix Obstetrics label corruption and narrow Trust-centres validator after SESSION_LIMIT=1000 run surfaced two validator FAILs
type: wrap-up
tags: [MD-304, data-pipelines, bug-fix, validator, trust-pipeline, plot-helpers, eda-notebook]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief/data_pipelines
    commit: 1f9dd07
  - path: /Users/rowanreid/.claude
    commit: 010b8d8
domain: medbrief
---

## Session Summary

Ran the Trust-centre pipeline at SESSION_LIMIT=1000 (Run 5 in the scaling
sequence), then ran the validator which reported 4 FAILs. Investigation via
direct DB queries showed two real bugs. First, `plot_claim_categories` in
`eda.ipynb` was mutating the DataFrame passed in when `obstetrics_group=True`,
collapsing every `'Obstetrics - <subcategory>'` label to bare `'Obstetrics'`.
Because `plot_eda(df)` ran before `df.to_csv(...)` in `main()`, every CSV
handed to training had lost obstetric subcategory granularity. All five prior
run folders (1510, 1525, 1554, 1603, plus the pre-fix 1603 re-run) exhibit
this. Fixed by computing the collapse on a local Series, leaving the caller's
DataFrame untouched.

Second, the validator's `check_trust_centres` asserted every row matched one
of four SQL wildcard tokens. But the SQL's primary inclusion branch is
`centretype = 1`, so legitimate NHS Trust rows (Guy's and St Thomas',
Imperial, etc.) were being flagged as invalid. Narrowed the CSV-only check
to "row has at least one centre name" (the only invariant the CSV can
verify), and added a new DB-backed `1b. Centre inclusion split` check that
queries `batchrequest` per session and reports the centretype=1 vs
wildcard-fallback breakdown.

Verified end-to-end: fresh SESSION_LIMIT=1000 run produced 9 distinct
obstetric subcategory labels in the CSV (not bare 'Obstetrics'), validator
went from 15 PASS / 4 FAIL to 31 PASS / 1 FAIL. The remaining FAIL ("Not
destroyed" — 15 destroyed batches across 6 sessions) is a pre-existing real
data issue unrelated to the two fixes. Both fixes committed as `1f9dd07`.
Memory updated in `~/.claude` to flag that pre-1755 training artefacts in
`preprocessed_data/` carry the corrupted labels and should be regenerated
before reuse.
