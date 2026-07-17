---
date: 2026-07-17
project: /Users/Rowan.Reid/claude_code/medbrief-work
domain: medbrief
session: AI-2066 external research reconciliation, roadmap restructure, handoff to Phase 3
type: handoff
tags: [ai-2066, translation, medbrief, deep-research, roadmap, handoff, azure, governance]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-work
    commit: af3d7cb8dd0f7b0975f7dcf905097f57c43d5475
model_check: fired-upgrade (model)
---

## Session Summary

Reconciled an external GitHub Copilot deep-research pass into AI-2066's four core docs (OVERVIEW, SOURCES, DESIGN-NOTES, BENCHMARK), catching and fixing a display-model error along the way, then restructured PLAN.md's stale Phase 3/4 into a sequenced Phase 3-6 roadmap. Also covered MedBrief's account-governance process for new translation-vendor sign-ups (AWS/Google/DeepL) and a PDF-support/effort analysis for each. Handed off to a fresh session scoped to Phase 3's Claude-executable checks only.

## Continuation Prompt

## Continuation: AI-2066 Phase 3 de-risking checks (API-version reconfirmation + comprepseudo German check)

**Parent session:** 2026-07-17-ai2066-research-reconciliation-and-roadmap.md

### Context
AI-2066 is MedBrief's translation workstream (German medical records to English, via Azure Document Translation for client "Compre"). The parent session reconciled an external GitHub Copilot deep-research pass into the ticket's four core docs and restructured `docs/ai-2066/PLAN.md` into a sequenced Phase 3-6 roadmap. This session picks up **only the Claude-executable slice of Phase 3**: two checks confirmed feasible without Rowan present (Azure CLI already authenticated, harness and fixtures already exist), explicitly excluding the two Phase 3 items that need Rowan (a Microsoft support ticket needing his portal login, and AWS/Google/DeepL account sign-ups needing his payment card and a message to a colleague).

### What was done this session (the parent)
- Read the external research findings and reconciled them into `OVERVIEW.md`, `SOURCES.md`, `DESIGN-NOTES.md` (new §17 on Apryse's XLIFF capability, §18 on the Branch A/B architecture split), and `BENCHMARK.md` (extended candidate set, corrected Google/DeepL limits).
- Caught and fixed a real error made mid-session: `DESIGN-NOTES.md` §18 had described the "reader sees English" branch as parallel bilingual display, which Deon explicitly ruled out on 10 July ("we ingest and translate, and then it's the English thereafter"). Fixed in place; the open question to Deon is now correctly scoped to the *artefact* (PDF file vs text layer), not the *display* (already decided: single-language).
- Restructured `PLAN.md`: replaced the stale Phase 3 ("evaluate against English pages") / Phase 4 ("recommendation") with a sequenced Phase 3 (cheap de-risking checks) through Phase 6 (build, split between what AI-2066 owns and what it only feeds into pseudonymisation's shared layer), plus a parallel compliance track.
- Confirmed this machine can execute Phase 3 items 1 and 3 directly: `az account show` returns `MedBrief Secure Review` (authenticated), `docs/ai-2066/harness/batch_translate_demo.sh` plus non-PHI fixtures exist at `data/ai-2066-demo/`, and `az cognitiveservices account show --name comprepseudo --resource-group AI_Resources` returns a reachable `TextAnalytics F0` resource.
- Committed `af3d7cb8dd0f7b0975f7dcf905097f57c43d5475` (medbrief-work, not pushed, per convention this repo is never auto-pushed by wrap-up).

### Current state
- `medbrief-work` on `main`, commit `af3d7cb8dd0f7b0975f7dcf905097f57c43d5475` (docs only, not pushed).
- `docs/ai-2066/PLAN.md` Phase 3 is the live task list. Items 1 and 3 are this session's job; item 2 (Microsoft support ticket) is a bonus if time allows (draft only, don't submit); item 4 (vendor sign-ups) is explicitly out of scope.
- Azure CLI authenticated to `MedBrief Secure Review` subscription on this machine already (confirmed working in the parent session; re-verify with `az account show` at the start of this session in case the token has expired).
- Non-PHI fixtures exist at `data/ai-2066-demo/`: `de-sample-arztbrief.pdf` (digital), `de-sample-arztbrief-scanned.pdf` (image-only scanned variant), plus prior English outputs from the earlier (2024-05-01-pinned) run for comparison.

### Where we left off
Nothing executed yet on Phase 3 itself; the parent session did the doc reconciliation and roadmap restructure, then handed off immediately. This session starts cold on the actual checks.

### Next steps
1. **PRIMARY: re-run the Phase 2b synthetic demo tests pinned to the CURRENT Azure API version.** `SOURCES.md`'s "API-version discrepancy" note and `DESIGN-NOTES.md`'s top-of-file 2026-07-17 update explain why: the currently-published Azure docs (`2026-03-01`) describe batch PDF translation as now routing through Azure Document Intelligence, but the existing findings were tested against `2024-05-01`. Use `docs/ai-2066/harness/batch_translate_demo.sh` and `harness/README.md` against the existing fixtures in `data/ai-2066-demo/`. Compare against the EXACT existing findings recorded in `SOURCES.md` (search for "Finding 1" and "Finding 2", and the equivalent text in `PLAN.md` Phase 2b): the dropped Diagnosis sentence on the digital path, and the line-fragmentation/lost-formatting/degree-symbol/untranslated-banner defects on the scanned path. Does the current API version still reproduce them, fix them, or change them? Write the result into `SOURCES.md` and `DESIGN-NOTES.md` §10 as a new dated update (follow the existing pattern of dated, additive corrections, never silently rewrite a prior finding). Update `OVERVIEW.md`'s open item and `PLAN.md` Phase 3/4 accordingly (Phase 4 item 6, the real-sample ground-truth run, is explicitly gated on this landing first, don't let it proceed until this is done).
2. **SECONDARY: check `comprepseudo`'s German PII-detection support.** This resolves `DESIGN-NOTES.md` §13's open ordering question (translate-then-pseudonymise, or the reverse). Resource confirmed reachable: `TextAnalytics F0`, endpoint `https://comprepseudo.cognitiveservices.azure.com/`, resource group `AI_Resources`, `MedBrief Secure Review` subscription. Test with **non-PHI synthetic German text only** (invented names/dates, nothing real) against the PII-detection API with `language=de`; confirm whether it reliably detects PII entity types in German. Write the finding into `DESIGN-NOTES.md` §13.
3. **OPTIONAL, only if time remains: draft (do not submit) the Microsoft support-ticket content** for the six Translator Docker container questions already listed in `SOURCES.md` (search for "written-confirmation questions"). Save the draft under `docs/ai-2066/` (e.g. `DRAFT-microsoft-support-ticket.md`, following the existing `DRAFT-teams-message.md` naming convention) for Rowan to review and submit himself; he holds the Microsoft support portal access and this agent should not attempt to file it.

**Explicitly out of scope, do not attempt:** Phase 3 item 4 (AWS/Google/DeepL trial sign-ups, notifying Chris Fuller), anything from Phase 4 onward, and anything touching real PHI (case 44240). This is non-PHI de-risking work only.

### Key references
- `docs/ai-2066/PLAN.md` (Phase 3 section is the task list)
- `docs/ai-2066/SOURCES.md` (API-version discrepancy note, the exact existing findings text, the six container questions)
- `docs/ai-2066/DESIGN-NOTES.md` §10 (mixed-document/omission findings, to be re-tested), §13 (the ordering question)
- `docs/ai-2066/harness/README.md` and `harness/batch_translate_demo.sh`
- `data/ai-2066-demo/` (non-PHI fixtures, gitignored)
- People: Deon Kuhn (CTO), Laura Gongas (ticket creator), Chris Fuller (IT/Compliance, not relevant to this session's scope but named in PLAN.md item 4)

### Notes for next session
- PHI guard rails in `PLAN.md` still apply in full: nothing in `data/` or the harness gets committed, no PHI in git commits/logs/shared output. This session's work is non-PHI only, so the guard rails constrain what NOT to touch (case 44240) rather than anything this session will actually do.
- If `az account show` fails (token expired), stop and tell Rowan rather than attempting to re-authenticate blind, that's a human step.
- Follow the existing doc convention throughout this ticket: corrections are dated and additive (a callout or an inline note), never a silent rewrite of a prior finding, even when the prior finding turns out to be superseded.
