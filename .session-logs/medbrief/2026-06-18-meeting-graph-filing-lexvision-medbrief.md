---
date: 2026-06-18
project: claude-code-demo1
domain: medbrief
tags: [meeting-graph, graph-to-notes, lexvision-poc, medbrief-onboarding, vault-coupling, harden-plan]
repos:
  lexvision-poc: 17a3b57
  medbrief-onboarding: 87cea12
  obsidian-vault: c427a57
model_check: not-needed
---

# Meeting-graph filing into lexvision-poc + medbrief-onboarding

Filed the processed meeting-graphs into their projects, correcting the starting premise. Investigation (3 parallel Explore/general agents) plus a /harden-plan pass over the plan showed only 3 of 5 graphs were genuinely unfiled: the 28 May (kumulus-medbrief) and 1 June (data-engineering) Kumulus meetings were ALREADY hand-curated in `lexvision-poc/docs/kumulus/03-meeting-*.md` and `04-meeting-*.md` (a rich dossier, notes 00-10 + audit + research/), and a delta-check of each graph against those notes + the dossier found ZERO genuine gaps - so they were left as-is, not re-filed. The 12 June Kumulus regroup was genuinely new and was filed as a curated dossier note `docs/kumulus/11-meeting-2026-06-12-regroup.md`; the two MedBrief product-walkthrough demos (Chantel van Wyk presenting) were filed into `medbrief-onboarding/notes/meetings/`. Each filed note carries a frontmatter `graph_ref` pointer.

Routing was project-only: nothing written to the strategic vault bar one coupling edit (the exact mis-route failure mode the 2026-06-13 calibration hit was avoided; verified the vault stayed clean). The /harden-plan pass (4 critics + pre-mortem) earned its keep - it caught a real vault-write hole (the `/graph-to-notes` `/decision-log` handoff still writes `Decisions/LOG.md` under `--dest project`, so the decision-log offer was declined throughout) and a curated-doc heading-match collision that proved real on the dry-run (default routing wanted 24 quotes threaded into the dossier, 4 into the protected `research/` subtree). Rowan chose record-over-threading, so each meeting landed as a single dated record. Also vault-coupled `lexvision-poc` (the hub note `Projects/lexvision/LexVision POC.md` gained a `## Detailed working project` down-link section; the project gained `docs/SOURCES.md` and a CLAUDE.md coupling section). Commits: lexvision-poc 17a3b57, medbrief-onboarding 87cea12, vault hub c427a57. One observed learning recorded (graph-to-notes record-over-curated-threading).
