# Next Up

## Now (Medbrief)

### Expert Sheet — Phase 1 + profile-gen done, Phase 2 (dedup) next
- **Last touched:** 2026-06-01
- **Status:** Phase 1 classification done (`data/experts_classified_20260601_152155.xlsx`; 1,021 medical experts, 1,098 law firms, 348 unknowns; cols P–U ours, col L untouched). Phase 1.5 profile generation built + test-run: `generate_profiles.py` produced a 30-row stratified batch (`data/experts_with_profiles_20260601_161909.xlsx`) appending Laura's Title-Case hand-off schema (doubles as de-dup signal). Cost ~$0.026/profile → ~$26 for the 1,000 medical-experts-not-in-MM pool; grounding only ~6% (verifiability flag for Laura).
- **Next action:** Phase 2 — build `detect_duplicates.py` (normalise → block → score → group → adjudicate → write cols V+) per the handoff continuation prompt, adapting `~/.claude/plans/whats-next-for-this-cozy-whistle.md`. In parallel: send `chantel_update.docx` + upload the classified xlsx to Chantel; confirm with Laura whether profile generation is Rowan's scope before any full profile run; triage the 348 unknowns later.

## Parked

## Done
