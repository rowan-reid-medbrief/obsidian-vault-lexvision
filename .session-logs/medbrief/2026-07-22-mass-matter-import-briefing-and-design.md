---
title: "Mass Matter Import: briefing ingest + gh-copilot design pass"
type: handoff
domain: medbrief
created: "2026-07-22"
parent: null
tags: [session-log, medbrief, mass-matter-import, gh-copilot]
---

# Mass Matter Import: briefing ingest + gh-copilot design pass

## Session summary

Ingested Deon's 2026-07-22 briefing for a new MedBrief short-term project (bulk-import the client Higgs' matters and radiology/hospital records) through the full meeting-graph pipeline, and scaffolded `docs/mass-matter-import/`. With Claude tokens scarce, offloaded the entire design pass to gh-copilot: six consults (~1,167 credits) produced blueprint, resilience, dev-environment, compliance and an adversarial-verification document, using a generate-broad-then-falsify pattern. The verification pass found the load-bearing gap nobody else caught: `Project::setManager()` grants no authorisation, so a naive console import would create matters nobody can access.

## Continuation Prompt

## Continuation: Mass Matter Import - resolve the three blockers, then build Phase 1

**Parent session:** 2026-07-22-mass-matter-import-briefing-and-design.md

### Context
New MedBrief short-term project, briefed by Deon Kuhn to Rowan on 2026-07-22: a one-off bulk import of the client **Higgs**' matters plus radiology and hospital records into MedBrief. No tracker ticket exists yet (Jira and Azure DevOps both checked); docs sit under `docs/mass-matter-import/` with a provisional slug. Architecture decided: build it as a Symfony console command IN the product codebase (`repo/`), not standalone Python. All working detail is in the repo; this prompt is the pointer.

**Token posture for the next session: keep making aggressive use of `/gh-copilot`.** Claude subscription is limited; MedBrief Copilot credits are plentiful. The proven pattern this session: write a precise brief to a `.task` file, dispatch `consult` with `--timeout 1800` detached in the background, redirect the envelope to a file so the large output never enters Claude's context, then spot-check only the load-bearing claims. Briefs are preserved in `docs/mass-matter-import/copilot-briefs/` and are re-runnable.

### What was done this session
- Fetched the SharePoint recording (`/fetch-video`, Chrome cookies; the direct-file grab returned an access page, so forced the DASH stream) and ran it through `/meeting-graph` end to end. Visual layer deliberately skipped: the screen share showed live client matter directories with real patient names.
- Wrote the meeting recap and scaffolded the ticket dir: OVERVIEW, PLAN, DESIGN-NOTES, SOURCES, IDEAS, meetings/.
- Confirmed via gh-copilot that MedBrief is Symfony/PHP; the "processing queue" is just `Disc.status` polled by cron; there is no import counterpart to `BulkMatterExportService`.
- Ran six gh-copilot consults (~1,167 credits total): BLUEPRINT, RESILIENCE, DEVENV, COMPLIANCE, and an adversarial VERIFICATION pass. All five documents are in `docs/mass-matter-import/`, each header-flagged as generated/unverified.
- Raised the gh-copilot wrapper's consult/review default timeout from 300s to 900s (a real brief was killed at 300s) and rewrote its timeout guidance. Committed and pushed to `~/.claude`.

### Current state
- **Workspace** (`~/claude_code/medbrief-work`): committed at `109df0b` (local-only repo, no remote by design). Clean.
- **Config** (`~/.claude`): committed and pushed at `0805cf1` (gh-copilot timeout + offload ledger).
- **Meeting-graph output**: `~/meeting-graph-output/mass-matter-import-2026-07-22/` (gitignored, outside the repo; not promoted to the vault store, by choice - a brand-new project has nothing to diff against).
- Project memory written: `project_mass-matter-import.md`.

### Where we left off
Design investigation is complete and verified. No code has been written. The next session starts by resolving three blockers that MUST be settled before any matter-creation code, then can begin Phase 1 (read-only analysis of the client data).

### Next steps
In priority order (all are top of `docs/mass-matter-import/IDEAS.md`):
1. **The access-role gap (highest).** `Project::setManager()` grants no authorisation; the web flow adds `ROLE_PROJECT_{id}_PROJECTMANAGER` to the logged-in creator separately (`ProjectController.php:437-441`). A console command has no security token. Confirm how to grant the role from a command, or every imported matter is silently inaccessible. Spot-check this against the source first (it is a VERIFICATION.md finding, not yet independently confirmed by us).
2. **Which account.** `Project.account` is non-nullable (`Project.php:1449`) and a wrong value causes cross-tenant exposure. The client sheet does not carry an account value; find where it comes from.
3. **Per-row transaction boundaries.** Nothing in the codebase wraps Project+Disc+Document creation as a unit; a mid-row crash leaves a valid but empty, permission-less matter.
4. Then Phase 1 in `PLAN.md`: parse the sheet, walk the tree (with our own symlink/realpath guards), classify each matter dir, produce a data-issues report. Read-only, no writes to MedBrief.
5. Still blocked on Deon: the client email chain, the anonymised test-radiology source, and (due 2026-07-23) the privileged Azure alias account.
6. **Friday 10:30 catch-up with Deon + Laura (2026-07-24):** raise the estate weaknesses in `RESILIENCE.md` §F5 and `DESIGN-NOTES.md` §8.3/§10.4 (stuck-disc sweep blind spot, no attempt counter, the access-role and notification gaps). Also flag the "expert mapping" vs "experts instructed" transcription uncertainty.

### Key references
- `docs/mass-matter-import/OVERVIEW.md` - start here.
- `docs/mass-matter-import/DESIGN-NOTES.md` - §8 (verified codebase findings), §9 (compliance obligations), §10 (the access-role gap). The load-bearing content.
- `docs/mass-matter-import/{BLUEPRINT,RESILIENCE,DEVENV,COMPLIANCE,VERIFICATION}.md` - generated, unverified, header-flagged. Read VERIFICATION.md before trusting the other four.
- `docs/mass-matter-import/copilot-briefs/` - the reusable `.task` briefs + README on re-running them.
- `docs/mass-matter-import/PLAN.md` - the phased build plan.
- Product code: `repo/` (Symfony/PHP, `git@github.com:medbrief/msr-medbrief.git`). Key files named throughout the docs with line numbers (accurate as of 2026-07-22; re-verify).
- People: Deon Kuhn (CTO), Chris (Azure alias account), Zach (local dev config guide + set up Rowan's VM), Adam, Laura (Friday catch-up).

### Notes for next session
- Every generated document carries line-number citations accurate on 2026-07-22 only; re-verify any specific line before building on it.
- The DEVENV.md guide (getting the radiology pipeline running locally) is the long pole for actually testing anything. Zach has a config guide Rowan does not yet have.
- Client data (real Higgs matters, patient-named directories) must NEVER touch Claude, Copilot, or Rowan's local machine. It may run on the DigitalOcean VM only. Keep all gh-copilot briefs about structure and code, never data.
