---
date: 2026-07-03
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: Coverage-graph reframe (output-neutral IR overlay) + first private GitHub remote + real corpus 3->11 docs; REMOVED margin rule built dormant
type: handoff
tags: [mri-133, medbrief, coverage-graph, harden-plan, matchers, corpus-expansion, github-remote]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 218f522
parent: 2026-07-03-mri133-split-frontiers-degraded-and-blank.md
model_check: not-needed
---

## Session Summary

Built the MRI-133 bipartite coverage-graph reframe as an output-neutral IR overlay (`matchers/coverage_graph.py` + `content_tokens.py`; `decide()` now a thin compat shim), planned and `/harden-plan`'d first, which correctly dropped the originally-planned capacitated-solver backbone (it could not be output-neutral, and the research report never wanted it as the backbone). Verified byte-identical via a committed 2160-prediction golden fixture, 290 tests, and the real bake-off (zero silent both populations, DoD GOOD, unchanged vs BASELINE.md); committed on `feat/coverage-graph-reframe` (218f522) and pushed to a newly-created private GitHub remote (`rowan-reid-medbrief/mri-133-annotations`, the repo's first). Also folded in the report's p7 REMOVED margin rule but shipped it DORMANT (dials default OFF), and expanded the real test corpus 3->11 docs from Azure across all four provenances (incl. two real image-only docs + a 1344pp trust doc), teeing up the next session's stamp+wire+measure build.

## Continuation Prompt

## Continuation: MRI-133 corpus-expansion build (stamp + wire, then measure)

**Parent session:** 2026-07-03-mri133-coverage-graph-reframe-and-corpus-expansion.md

### Context
MRI-133 PoC (medbrief), ~/claude_code/projects/annotations. Cardinality-aware page
reconciliation so annotations/redactions transfer when a records bundle is re-sorted. The
coverage-graph reframe is DONE and committed (output-neutral IR overlay); the real corpus was
just expanded 3->11 docs. This session's job: make the new docs usable, read the numbers.

### What was done last session
- First git remote: private GitHub `rowan-reid-medbrief/mri-133-annotations` (SSH via
  ~/.ssh/github, gh installed); pushed main + the feature branch. See [[mri133-github-remote]].
- Coverage-graph reframe as an OUTPUT-NEUTRAL IR overlay: `matchers/coverage_graph.py`
  (build+resolve, outcome read off node degree), token helpers -> `matchers/content_tokens.py`,
  `decide()` now a thin compat shim. Planned + /harden-plan'd (9-critic fan-out), which dropped
  the originally-planned capacitated-solver backbone (couldn't be output-neutral; the report
  reserves ILP for local clone/split, not the backbone).
- Report's p7 REMOVED margin rule folded in but shipped DORMANT: dials
  `removed_coverage_floor`/`removed_margin_min` default 0.0 (OFF); emits AMBIGUOUS, never a
  confident REMOVED.
- Verified: committed golden fixture (`tests/test_output_neutrality.py`, 2160 predictions)
  byte-identical before/after; 290 tests; real bake-off zero silent both populations, DoD GOOD,
  unchanged vs BASELINE.md. Committed on `feat/coverage-graph-reframe` (218f522), pushed.
- Real corpus expanded 3->11 docs from Azure (all four provenances; 2 real image-only docs + a
  1344pp trust doc), git-ignored in `poc/data/real-samples/`. See [[mri133-real-data-container]].

### Current state
- Branch `feat/coverage-graph-reframe` (218f522) pushed. `main` not yet merged (your call: PR at
  github.com/rowan-reid-medbrief/mri-133-annotations/pull/new/feat/coverage-graph-reframe, or
  merge locally).
- 11 raw real docs in `poc/data/real-samples/`; only the original 3 are stamped into
  `_stamped/*.clean.pdf` and wired into `real_bakeoff.py`. 290 tests green, tree clean.

### Next steps (priority order)
1. **[FIRST - stamp + wire]** Stamp the 8 new real docs into
   `poc/data/real-samples/_stamped/*.clean.pdf` (self-consistent re-stamped IDs + degraded
   variant, the same prep the original 3 had). NB the 2 image-only docs (`combined_100200`,
   `142257-12147`, 0% text) need the RENDER-based ID path, not text-hash. Then wire
   `scripts/real_bakeoff.py` to source all 11 (it currently only picks up the original 3).
2. Run the enlarged real bake-off (`--population both --by-case`); read the REMOVED/SPLIT/CLONE
   slices at the larger N.
3. Decide the dormant REMOVED rule's enable-gate: add the two adversarial REMOVED synthetic
   slices, calibrate `removed_*` holding silent-0, then enable or drop. (`[high]` in IDEAS.md.)
4. Optional: merge/PR the reframe branch; unpark the pagination fuse (`[parked] [high]`).

### Key references
- `docs/DESIGN-NOTES.md` 2026-07-03 (reframe + fidelity-to-research), `docs/IDEAS.md`
  (corpus-expansion + dormant-rule items), `docs/plans/before-numbers/BASELINE.md` (numbers to hold).
- Source: `matchers/{coverage_graph,content_tokens,decision,base}.py`, `config.py` (`removed_*` dials).
- Tests: `cd poc && .venv/bin/python -m pytest -q` (290). Bake-off:
  `.venv/bin/python scripts/real_bakeoff.py --population both --by-case`; synthetic `./mri133 run
  --population both --by-case`.
- Memory: [[mri133-cardinality-channels]], [[mri133-real-data-container]], [[mri133-github-remote]],
  [[mri133-venv-path]].

### Notes for next session
- Setup: sonnet/high is fine for stamp+wire (standard single-system coding); bump to opus/high for
  the enable-gate calibration if it gets fiddly.
- The stamp step is the one real unknown: check exactly how the original 3 `_stamped/*.clean.pdf`
  were produced (in `real_bakeoff.py` or a helper) and mirror it, watching the image-only render-ID path.
