# Next Up

## Now (Medbrief)

### gh-copilot delegation - programme COMPLETE, shakedown closed (2026-07-18)
- **Status:** probes 1+11 PASS in the fresh post-merge session; scoped `allowed-tools` adopted (SKILL.md v1.1, `last_shakedown` set); propose-and-paste offload spotter live on this machine (`a15c3cf`). `last touched` 2026-07-18.
- **next:** use it organically: the first pasted `/gh-copilot` proposal writes the offload ledger's first line; review checkpoint at ten ledger lines or 2026-08-17 (use-it-or-lose-it).
- [[2026-07-18-gh-copilot-post-merge-probes-and-offload-spotter]]

### MedBrief quarterly company meetings - ingested to vault
- **Status:** Q1 (March) and Q2 (June) 2026 company updates fully ingested via /process-meeting: meeting-graphs (183n/333e, 160n/314e) in ~/meeting-graph-output/, recaps in Resources/Summaries/medbrief/, March's two strategic decisions logged. Q2 Pass-3 chapters 07-08 hand-authored after a session-limit killed two subagents (03-04 salvaged from a valid .tmp). `last touched` 2026-06-26.
- **next:** Optional, neither blocks anything: log Q2's three decision candidates (equity rollout/valuation, grow-without-headcount, Athena agent) via /decision-log; regenerate the hand-built 07-08 edges via subagent for consistency.
- [[2026-06-26-quarterly-company-meetings-ingestion]]

- MRI-133 "Granular storing of pages" (Track B: round out the content arm; matcher-arm profiled + closed-form `_fit_axis` fix shipped; content-arm DoD MARGINAL, last touched 2026-07-10)
  next: resume Track B #1 (corpus expansion + uncap the giants, gated by matcher-arm perf). Re-run the corpus-scale timed bake-off (killed mid-run) to decide whether to vectorise the cross-section split RANSAC (logged [med] in docs/IDEAS.md); corpus expansion needs Deon's Azure Blob / jumpbox access. Full 5-step build order in docs/IDEAS.md [plan] entry. NB programme spine still stale (last_synced 2026-06-23).
  [[2026-07-10-mri133-content-arm-perf-track-b]]

- Apprise viewer date-range rendering (MRI-134) (copy elimination + cap removal committed and pushed, benchmark table verified, last touched 2026-07-10)
  next: **send Deon the benchmark table and the branch** (`feature/MRI-134-pdf-split-approach`, tip `27547ede3`, both fixes pushed). The "~19x MedBrief overhead" was disproven (a page-cache confound from the whole-file copy); PHP-Apryse and Python-Apryse tie, PyMuPDF is disqualified. Then decide async subset generation vs a config-bound product page limit: the request wall is nginx's 60s fastcgi default and php-fpm has only 5 workers. The subset cache still has no eviction (~2.9GB per 10k subset). VM has ~30GB throwaway fixtures in `/var/tmp/mri134` to clean. Workstream B (date-range -> page mapping via `ChronologyItem` Bates refs) is still the real feature blocker.
  [[2026-07-10-mri134-copy-elimination-and-cap-removal]]

- Translation | Compre (AI-2066) (external deep-research pass reconciled into all four core docs; PLAN.md restructured into a sequenced Phase 3-6 roadmap; last touched 2026-07-17)
  next: handed off to a fresh session for Phase 3's Claude-executable checks (API-version reconfirmation, comprepseudo German-support test). Phase 3 item 4 (AWS/Google/DeepL sign-ups, tell Chris Fuller) is still Rowan's own action.
  [[2026-07-17-ai2066-research-reconciliation-and-roadmap]]

### MedBrief onboarding - knowledge-share deck + branded pack
- **Last touched:** 2026-06-19
- **Status:** Rebuilt the knowledge-share deck via the upgraded medbrief-brand skill, folding Rowan's hand-tuned font sizes into a 14pt PPTX body-text floor (`build_pptx`). Built a de-identified, em-dash-free public onboarding pack from `onboarding-pack-v1` (`medbrief-overview-public.{md,docx,spec.json}`): all individuals removed, external orgs (client firms, NHS Trusts, UCL) generalised, personal-onboarding framing stripped, ticket/Confluence IDs kept. Further hardened the skill: `md_to_spec` drops thematic breaks, folds wrapped list-item continuations, and parses inline markup in table cells; `build_docx` renders table-cell runs and restarts numbering per list. Tests 47/47; ~/.claude scripts committed + pushed, project deliverables committed.
- **next:** Rowan reviews `output/medbrief-overview-public.docx` + the rebuilt `output/knowledge-share-deck.pptx`. Open: sweep em dashes from the deck `.md` (14 left); optionally add inline-code styling / full inline-in-table support to the skill. Install Degular for true-brand headings.
- [[2026-06-19-public-onboarding-pack-and-brand-skill-fixes]]


### Kumulus / MedBrief engagement (lexvision-poc)
- **Status:** Gen 4 "Data and AI PoV" (received 9 Jul) reviewed + documented (review doc `12-review-2026-07-09-data-ai-pov.md`, ADR-009). Scope inverts back to the d1 split: Kumulus builds the upstream extraction pipeline (M2-M7), drops OCR + the comparison layer; MedBrief keeps the reasoning layer. Position: hold accept-in-principle-and-negotiate. `last touched` 2026-07-16.
- **next:** Take the five open items to Kumulus/Laura/Deon: (1) settle the data-handoff de-identification state + Azure tenancy FIRST (new compliance crux: prepared case data crosses to a Brazil-based vendor); (2) IP transfer of extraction/pseudonymisation notebooks + schema; (3) incentive-failure fallback in writing; (4) numeric acceptance bars per ADR-004; (5) reconcile the pricing-slide-vs-body comparison contradiction. Confirm the Gen 4 deck supersedes the 10 June one.
- [[2026-07-16-kumulus-gen4-data-ai-pov-review]]

### NICE guideline access for the Kumulus case set (lexvision-poc)
- **Status:** Laura asked Rowan to check whether the NICE guideline versions the Kumulus cases actually need are obtainable via the new NICE API trial, which seems to expose only current versions. `last touched` 2026-07-17.
- **next:** identify which NICE guideline version(s) the actual Kumulus cases reference (via MedBrief clinical summaries/chronologies/ECAs), then check NICE API coverage; if unavailable, prototype scraping + local storage. Separately unresolved: whether a NICE-guideline link found in an unrelated case's clinical summary is a genuine clinical citation or generic appendix content.
- [[2026-07-17-narrate-meeting-shakedown-nice-ai2066]]

### Expert Sheet — Phase 2 dedup, pending USE_DB run + Chantel delivery
- **Last touched:** 2026-06-09
- **Status:** Phase 2 `scripts/detect_duplicates.py` built, validated, committed. Full AI adjudication (1,864 medium pairs) **intentionally gated on profile data** — Gemini has no new signal without specialty/location data. **Since (2026-06-04):** shared `OUTPUT_MODE`/`WORKING_FILE` env flags + non-overlapping column blocks (P1 P–U, P2 V–Z, P1.5 AA onward; commit `06cb9b5`); project restructured to `scripts/` + `data/{raw,interim,outputs}` + `docs/` + `deliverables/` with repo-root path anchoring + `README.md`/`requirements.txt` (commits `6a58c07`, `f6d3ddb`); 3 legacy outputs consolidated into canonical `data/outputs/experts_working.xlsx` via `scripts/combine_outputs.py` (commit `effe70a`). Works **on `main` only**. **Since (2026-06-05):** verified `experts_working.xlsx` faithfully consolidates all 3 phases (P1 cols Q–U 2,810 rows, P2 V–Z 5,480 rows, P1.5 AA–BF ~30-row test batch) and **deleted the 3 legacy output workbooks** — working file is now the sole canonical output. **Substantially finalised `deliverables/chantel_update_phase2.docx`** (commit `90d5703`): single side-by-side user-type model-comparison table (1 June `gemini-2.5-flash` vs 4 June `gemini-3.1-pro-preview` — newer model more cautious, 348 unknowns vs 252, +134 law firm); plain "Summary" with row-numbered real examples; new "Profiles" section; removed the pasted dup-score/keep scratch from below the sign-off. (Heads-up: discovered python-docx `doc.paragraphs` hides tables — the "Column W"/"Results" headings were never empty; new profile rule saved.)
- **SDD assessment + pytest gate (2026-06-05):** Assessed Spec-First L1, gated at L0 by absent tests. Pytest recall gate **implemented** same session (commit `a4d6721`): 18/18 passing; project now Spec-Anchored. Run `venv/bin/pytest -v` to verify.
- **Next action:** (1) Finish the docx polish before sending — fix the broken sentence in the dup-detection intro ("…but since it focusses on… I wrote the script also catch…"), resolve the dangling "more on this below" in the Medium-tier bullet, tidy the pre-existing bold inconsistencies, and fill the `[SharePoint link]` placeholder. (2) Run USE_DB=true deterministic pass — open the jumpbox SSH tunnel first (command + `Not Found` fix now in `docs/DB_TUNNEL.md`; pre-staging port 3310), then `DEDUP_DRY_RUN=false DEDUP_ADJUDICATE=false DEDUP_USE_DB=true venv/bin/python3 scripts/detect_duplicates.py`. (3) Deliver `data/outputs/experts_working.xlsx` + the finalised docx to Chantel. (4) Confirm with Laura whether full profile generation is Rowan's scope (gates the AI adjudication step). Also open: triage the 348 Phase-1 unknowns.

### MedBrief Data Strategy
- **Last touched:** 2026-06-25
- **Status:** Discovery. Frontier Week project-relevance digest delivered: ~47-min spoken audio (Daniel voice) of the three talks, theme-woven and led by the data strategy, in iCloud (`Frontier-Week-Digest/`) + transcript `notes/frontier-week-digest-2026-06-22.md`. Advisory follow-on: Fabric is a leading-but-not-chosen candidate (even Microsoft frame it as unify-on-OneLake, keep Databricks); pseudonymise at egress / third-party hand-off, not on ingest into your own OneLake (still personal data; use a locked landing zone + apply-security-once masked views, physical de-id only at egress, a Deon + DPO call); the talks re-open Fabric for the Kumulus track per-module (most concretely ADR-002's graph store as a new Azure-native candidate, plus MedBrief's new prep-zone/de-id responsibility), not the narrow current PoV.
- **next:** Raise the standard agent-to-data interface (MCP) against the MSR MCP server epic (MSR-5832) as buy-vs-build (strongest follow-up). Carry Fabric (apply-security-once, AI-on-PDF, works-with-Databricks) into the Dot Collective (26 June, Jack Ford) + Kumulus evaluation as a baseline. Fold the ontology cross-check + Fabric graph DB into ADR-002. Start data-source discovery across the customer/product/people cycles.
- [[2026-06-25-frontier-week-relevance-digest-and-fabric-qa]]

## Now (Personal)

### Claude Code config modernisation: Phase A done, B/A6/C1 remain
- **Last touched:** 2026-06-07
- **Status:** Deep feature audit of the ~/.claude setup, hardened via /harden-plan into a lean-spine plan (gitignored at ~/.claude/plans/please-can-you-do-elegant-bubble.md). Phase A committed and pushed (30e5899, 89f8ef3): python3 status line (renders next session), `memory: user` on config-auditor and obsidian-curator with agent-memory/ gitignored first, /context pointers in wrap-up/handoff. Findings: fallbackModel is a `--fallback-model` CLI flag not a settings key; A5 SessionEnd dropped (no safe job). 7 high-priority remaining items in ~/.claude/docs/IDEAS.md (2026-06-07).
- **Next action:** Run Phase B (CLAUDE.md reclassify-and-trim) in a FRESH session: build the before/after adherence fixture FIRST (about 8 prompts plus negative probes that bait the wrong behaviour, run on a bare session), classify rules never-delegate vs may-delegate, keep safety/voice/account rules inline, target under 200 lines. Then the A6 sandbox pilot (keys in IDEAS.md) and the C1 auto-memory decision.

## Parked

- **MedBrief workspace consolidation** - completed 2026-07-09: apprise-viewer-rendering renamed to `medbrief-work`, the msr-medbrief checkout nested as a gitignored `repo/`, the mutagen sync terminated and recreated on the new alpha path, both memory slugs merged under the workspace slug, and the vault hub pointer plus `docs/SOURCES.md` repointed. Stages 2-5 all proven. [[2026-07-09-medbrief-workspace-consolidation-stages-2-5]]
- **demo-walkthrough `cli` frame** - C1-C3 shipped 2026-06-29: a first-class terminal frame for command-line tools - the static renderer (C1), the contained live-capture orchestrator (C2: `capture_cli.py` + the shared `containment.py`, an env-allowlisted sandbox with per-command mutation proofs; mri133 the worked tool), and the SKILL.md wiring + reference + `test-cli-e2e.sh` (C3). C4 (typing animation) is the deferred fast-follow. [[2026-06-29-demo-walkthrough-cli-frame-c2-c3]]
- **MedBrief walkthrough + Kumulus meeting-graph filing** - done 2026-06-18: 3 meetings filed (2 MedBrief demos -> medbrief-onboarding/notes/meetings/, Kumulus regroup -> lexvision-poc dossier), 2 Kumulus meetings (28 May, 1 June) delta-checked clean (already hand-filed), lexvision-poc vault-coupled. [[2026-06-18-meeting-graph-filing-lexvision-medbrief]]

## Done
