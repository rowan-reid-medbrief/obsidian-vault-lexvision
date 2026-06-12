# Next Up

## Now (Medbrief)

### MedBrief onboarding - product walkthrough meeting-graphs
- **Last touched:** 2026-06-12
- **Status:** Fetched Chantel's two walkthroughs from SharePoint and built two meeting-graphs (219 nodes/529 edges; 306/749) in `~/meeting-graph-output/`, covering the full feature surface and the matter-creation flow. Transcribed with MLX large-v3-turbo on the GPU.
- **next:** Fold the two walkthrough graphs into the project `notes/` via `/graph-to-notes` and add `docs/SOURCES.md` up-links (idea logged in `docs/IDEAS.md`).
- [[2026-06-12-medbrief-walkthrough-graphs-and-mlx-wiring]]

### MedBrief onboarding - ADO repos, vault coupling, brand skill
- **Last touched:** 2026-06-09
- **Status:** Found ADO (`MedBrief AI`) hosts 12 git repos (the AI team's primary code host); corrected notes/00,07,08 + saved a memory. Coupled the project to the vault (hub note `Projects/medbrief/MedBrief Onboarding.md`, added to the Coupled list). Built the `medbrief-brand` skill (branded docx/pptx, teal #009999 / green #72CC52 tokens, logos incl. white variants) + `notes/13` brand research; QA'd via newly-installed LibreOffice.
- **Next action:** Resolve the brand palette (corporate teal/green vs product indigo #5E53D1); request access to GDES-174 "Templates" + the Drive/Figma brand masters to harden the skill's type scale and logo clear-space. Onboarding pack still at v1 intermediate notes.
- [[2026-06-09-medbrief-onboarding-ado-coupling-brand-skill]]


### Kumulus / MedBrief engagement (lexvision-poc)
- **Last touched:** 2026-06-12
- **Status:** Working doc renamed `Landing Pad.docx` → `Rowan Kumulus Research.docx` and hand-edited in Rowan's voice: patent and ADR/decision reference numbers removed, M3–M12 benchmark cells narrated (links kept), GLiNER/Presidio cells clarified, M2 typo fixed. ~15 voice patterns captured to `~/.claude/profile/writing-voice.md`. The `landing-pad.spec.json` generator is now stale; do NOT rebuild (would wipe manual edits).
- **next:** Send the corrected `Rowan Kumulus Research.docx` to Laura and Deon; confirm the 15 June 15:00 Dublin slot with João; retire/reconcile the stale Landing Pad generator (IDEAS.md); resolve the ~/.claude cross-machine divergence; chase the named residuals (Deon, NICE in writing, Agilio).
- [[2026-06-12-kumulus-tone-profile-and-landing-pad-edits]]

### Expert Sheet — Phase 2 dedup, pending USE_DB run + Chantel delivery
- **Last touched:** 2026-06-09
- **Status:** Phase 2 `scripts/detect_duplicates.py` built, validated, committed. Full AI adjudication (1,864 medium pairs) **intentionally gated on profile data** — Gemini has no new signal without specialty/location data. **Since (2026-06-04):** shared `OUTPUT_MODE`/`WORKING_FILE` env flags + non-overlapping column blocks (P1 P–U, P2 V–Z, P1.5 AA onward; commit `06cb9b5`); project restructured to `scripts/` + `data/{raw,interim,outputs}` + `docs/` + `deliverables/` with repo-root path anchoring + `README.md`/`requirements.txt` (commits `6a58c07`, `f6d3ddb`); 3 legacy outputs consolidated into canonical `data/outputs/experts_working.xlsx` via `scripts/combine_outputs.py` (commit `effe70a`). Works **on `main` only**. **Since (2026-06-05):** verified `experts_working.xlsx` faithfully consolidates all 3 phases (P1 cols Q–U 2,810 rows, P2 V–Z 5,480 rows, P1.5 AA–BF ~30-row test batch) and **deleted the 3 legacy output workbooks** — working file is now the sole canonical output. **Substantially finalised `deliverables/chantel_update_phase2.docx`** (commit `90d5703`): single side-by-side user-type model-comparison table (1 June `gemini-2.5-flash` vs 4 June `gemini-3.1-pro-preview` — newer model more cautious, 348 unknowns vs 252, +134 law firm); plain "Summary" with row-numbered real examples; new "Profiles" section; removed the pasted dup-score/keep scratch from below the sign-off. (Heads-up: discovered python-docx `doc.paragraphs` hides tables — the "Column W"/"Results" headings were never empty; new profile rule saved.)
- **SDD assessment + pytest gate (2026-06-05):** Assessed Spec-First L1, gated at L0 by absent tests. Pytest recall gate **implemented** same session (commit `a4d6721`): 18/18 passing; project now Spec-Anchored. Run `venv/bin/pytest -v` to verify.
- **Next action:** (1) Finish the docx polish before sending — fix the broken sentence in the dup-detection intro ("…but since it focusses on… I wrote the script also catch…"), resolve the dangling "more on this below" in the Medium-tier bullet, tidy the pre-existing bold inconsistencies, and fill the `[SharePoint link]` placeholder. (2) Run USE_DB=true deterministic pass — open the jumpbox SSH tunnel first (command + `Not Found` fix now in `docs/DB_TUNNEL.md`; pre-staging port 3310), then `DEDUP_DRY_RUN=false DEDUP_ADJUDICATE=false DEDUP_USE_DB=true venv/bin/python3 scripts/detect_duplicates.py`. (3) Deliver `data/outputs/experts_working.xlsx` + the finalised docx to Chantel. (4) Confirm with Laura whether full profile generation is Rowan's scope (gates the AI adjudication step). Also open: triage the 348 Phase-1 unknowns.

## Now (Personal)

### Claude Code config modernisation: Phase A done, B/A6/C1 remain
- **Last touched:** 2026-06-07
- **Status:** Deep feature audit of the ~/.claude setup, hardened via /harden-plan into a lean-spine plan (gitignored at ~/.claude/plans/please-can-you-do-elegant-bubble.md). Phase A committed and pushed (30e5899, 89f8ef3): python3 status line (renders next session), `memory: user` on config-auditor and obsidian-curator with agent-memory/ gitignored first, /context pointers in wrap-up/handoff. Findings: fallbackModel is a `--fallback-model` CLI flag not a settings key; A5 SessionEnd dropped (no safe job). 7 high-priority remaining items in ~/.claude/docs/IDEAS.md (2026-06-07).
- **Next action:** Run Phase B (CLAUDE.md reclassify-and-trim) in a FRESH session: build the before/after adherence fixture FIRST (about 8 prompts plus negative probes that bait the wrong behaviour, run on a bare session), classify rules never-delegate vs may-delegate, keep safety/voice/account rules inline, target under 200 lines. Then the A6 sandbox pilot (keys in IDEAS.md) and the C1 auto-memory decision.

## Parked

## Done
