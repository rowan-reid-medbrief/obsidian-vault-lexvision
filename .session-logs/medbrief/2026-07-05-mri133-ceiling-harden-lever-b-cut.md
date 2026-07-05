---
type: handoff
tags: [mri-133, annotations, content-arm, matcher, harden-plan, close-out, medbrief]
repos:
  - annotations: aedc907
parent: 2026-07-04-mri133-render-fix-and-clean-confirmation.md
model_check: not-needed
---

# MRI-133: ceiling read, plan hardening, and the Lever-B cut

Measured why the content-arm review queue sits at 31%: it is not systemic but concentrated in
repetitive/blank documents (bench-115131 = 168pp, 22 distinct texts, 42 blanks, 0 anchors on every
channel) that are information-theoretically content-unresolvable, so the planned sequence/neighbour
bracketing layer was hardened (/harden-plan, 13 critics) and then CUT by a corpus-wide go/no-go (0
bracketable middle; bimodal corpus). The actual queue fix is Lever A, median fusion, which converts
every weak-match over-abstain to a confident anchor (108->0); it plus the honest ceiling report is now
the whole deliverable, with the safety gate corrected from the far-too-loose "precision >= 0.95" to an
absolute zero-new-silent-error count on the full population. Lever A build and its two safety gates
are not yet done (carried into the continuation).

## Continuation Prompt

## Continuation: MRI-133 - build Lever A (median fusion) + its safety gates

**Parent session:** 2026-07-05-mri133-ceiling-harden-lever-b-cut.md

### Context
MRI-133 PoC: cardinality-aware page reconciliation so annotations/redactions transfer when a
medical-records bundle is re-sorted, WITHOUT a durable stamp (the content-only arm is the PRIMARY
goal). The content-arm ensemble sits at DoD MARGINAL (P99.9 / R69.0 / queue31.0); the goal is to
clear the review queue toward GOOD while adding ZERO new silent errors (each = a PII mis-transfer).

### What was done this session
- MEASURED why the 31% queue exists (three diagnostics + the confirmation JSON): it is NOT systemic.
  SAFE_ABSTAIN=0 (all 4792 queued pages are OVER_ABSTAIN); the queue concentrates in repetitive/blank
  docs. bench-115131 (168pp) = 22 distinct page-texts + 42 blanks -> every page has an exact content
  twin -> 0 unique-placement anchors on EVERY channel -> information-theoretically content-unresolvable.
- Ran the model-check (opus/high confirmed) and /harden-plan (13 critics, 87 findings). Key catch:
  "precision >= 0.95" tolerates ~555 PII mis-transfers, so the ship gate is now an ABSOLUTE
  zero-new-silent-error count on the FULL population, not the precision ratio.
- A corpus-wide GO/NO-GO CUT the sequence/neighbour layer (Lever B): 0 bracketable middle; the corpus
  is bimodal (per-doc anchor% under median = [100,99,0,99,68,89,100,97]). The bracketer had nothing
  to bracket.
- Found the actual fix: Lever A = MEDIAN fusion (per-cell median of exact_hash/perceptual/text_fp =
  trust a 2-of-3 agreement). Converts every weak-match over-abstain (fused ~0.667 under the old
  equal-weight MEAN, below tau_accept 0.80) to a confident anchor: measured weak 108 -> 0 across 8 text
  docs. Correctly leaves genuinely identical pages ABSTAINED (all 3 channels tie -> no false confidence).
- Committed the hardened plan + findings + a Deon finding (repetitive/blank docs need the stamp).

### Current state
- annotations commit `aedc907` on `feat/coverage-graph-reframe` (NOT main): the two plans docs + the
  IDEAS finding. NO source/matcher code changed yet.
- Vault committed + pushed (`9f37a6f`); memory `mri133-cardinality-channels` corrected.
- Single source of truth for the build: `plans/2026-07-04-sequence-layer-plan.md` (read the "GO/NO-GO
  OUTCOME" banner + "What hardened" delta first). Evidence: `...-ceiling-findings.md`.

### Where we left off
Design + measurement complete; the sequence layer is cut. Stopped BEFORE writing code: median fusion
changes the core signal for every page in every matcher (big blast radius) and its safety is
unverified, so it wanted a fresh, attended session.

### Next steps
1. [high] BUILD LEVER A (median fusion). Add a `fusion_rule` dial to `MatcherConfig` (default the
   median rule ON, pinned to `mean` in `_NEUTRAL_CFG` so the golden fixture stays byte-identical, the
   OCR/twin_split_abstain precedent). `EnsembleMatcher.match` (ensemble.py:61) reads it: per-cell
   median of the 3 member matrices instead of the equal-weight mean. Mechanical -> Sonnet/high.
2. [high] SAFETY GATE (both owed before ship): (a) a synthetic dial-ON scored run over DUPLICATE /
   FORM_LETTER / removed-look-alike archetypes -> ZERO new silent errors (median's risk is a
   2-of-3-dissent look-alike the mean safely abstained); (b) a real-corpus zero-new-silent bake-off
   (capture today's 7 silent-error page_ids from poc/data/real-bakeoff.json first; assert no new ids on
   the FULL population). The real run also settles headline-to-GOOD and folds in the 3 image-only docs.
3. [med] Write the honest ceiling for Deon as a one-off script (extend anchors2.py): repetitive/blank
   docs are content-unresolvable = stamp territory. GT-free partition key.
4. Carried backlog (already in docs/IDEAS.md): degraded-population pass, `--skip-degrade` flag, profile
   the matcher arm (the 44-min wall-clock), decide keep/drop the dormant REMOVED rule, OCR-at-ingestion
   to Deon.

### Key references
- Integration point: `poc/src/mri133/matchers/ensemble.py:61` (fusion line); `config.py` (MatcherConfig
  dials, the `_enable`/pin pattern); `tests/test_output_neutrality.py:49` (_NEUTRAL_CFG).
- Scorer facts: `scoring/metrics.py` (SILENT_ERROR bucket), `scoring/dod.py` (GOOD needs P>=0.95 &
  R>=0.70 & queue<=0.30; there is NO "PASS" reading, a parent-prompt error corrected this session).
- Two auto-decisions taken while away (reversible; confirm on pickup): ship-A-first / gate-B (settled:
  B is cut), and zero-new-silent (full population) as the safety gate.

### Notes for next session
- venv at poc/.venv; Bash cwd resets each call; use absolute paths. Bake-off JSON is at
  poc/data/real-bakeoff.json (NOT data/). IDEAS.md is at the REPO ROOT (docs/IDEAS.md).
- The median rule for 3 channels = 2nd-highest = drop-lowest-and-highest; keep it a single scalar per
  cell feeding finish() unchanged (hardening flagged that a "2-of-3 boolean" rule would NOT fit the
  scalar tau_accept/near-tie machinery).
- Real bake-off ~56 min; PYTHONUNBUFFERED=1 + a background run. macOS has no timeout/gtimeout.
