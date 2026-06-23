---
title: "Frontier Week: three knowledge graphs built and routed into data_strategy + lexvision-poc"
date: 2026-06-23
type: handoff
domain: medbrief
tags: [meeting-graph, graph-to-notes, frontier-week, data-strategy, lexvision, microsoft-fabric]
repos: [ObsidianVault, claude_code/data_strategy, claude_code/projects/lexvision-poc]
parent: 2026-06-22-frontier-week-ingestion-pipeline.md
model_check: not-needed
---

# Frontier Week: graphs built and routed

Built knowledge graphs for all three on-demand Microsoft Cloud and AI Frontier Week sessions (keynote 238 nodes/521 edges, Transform Data Silos 199/412, Turn Agentic AI 188/448) via /meeting-graph, including a full re-extraction of session 3 after diagnosing that the host sleeping mid-run (not an O(n^2) clustering blow-up) had stalled its diarisation; re-run under `caffeinate -i` and rebuilt turn-accurate. Routed the content with /graph-to-notes on the agreed split: structured per-session records into the MedBrief data_strategy project (`notes/` + `docs/SOURCES.md`), a targeted ontology/graph/agent tech slice into lexvision-poc (`docs/frontier-week-tech-learnings.md`, tied to ADR-002/003 + Kumulus), and hub-altitude pointers into both vault notes. Caught and cleared em-dashes from all authored content. Next: a ~45-minute project-relevance digest across the three sessions, rendered to audio via /work-digest (see continuation prompt).

## Continuation Prompt

## Continuation: Frontier Week project-relevance digest (research -> audio)

**Parent session:** 2026-06-23-frontier-week-graphs-and-routing.md

### Context
The three Microsoft Cloud & AI Frontier Week sessions (22 June 2026) are fully processed into knowledge graphs and routed into project notes. This session produces the next deliverable: a single spoken **digest** of what was in those talks, framed by relevance to each of Rowan's active projects, for him to listen to on a ~45-minute walk. Treat it as a research-and-synthesis exercise first, then render to audio.

### What was done (prior session)
- Built knowledge graphs for all three sessions via /meeting-graph: keynote (238 nodes/521 edges), Transform Data Silos (199/412), Turn Agentic AI (188/448). All diarised, turn-accurate.
- Routed via /graph-to-notes: per-session records into `data_strategy/notes/`, a tech slice into `lexvision-poc/docs/frontier-week-tech-learnings.md`, hub pointers into both vault notes.

### The task
Produce a ~45-minute, discussion-style spoken digest of the *content* of the three talks, tied back to Rowan's work. Two stages:

1. **Research / synthesis (do this first, present for review before rendering).**
   - Read the three meeting records in `~/claude_code/data_strategy/notes/frontier-week-*-meeting.md` (and the graphs/summaries in `~/meeting-graph-output/frontier-week-*-2026-06-22/` for depth).
   - For each of Rowan's projects below, pull out the *specific* product features, claims, and ideas from the talks that bear on it, and say how. Be concrete (name the feature, e.g. "Fabric IQ ontologies", "data agents grounded in an ontology", "OneLake security GA", "the intent economy"), not generic.
     - **MedBrief (broadly)** - the company-wide AI/data direction.
     - **medbrief-onboarding** (`~/claude_code/medbrief-onboarding`).
     - **MedBrief Data Strategy** (`~/claude_code/data_strategy`) - the primary fit; discovery phase, evaluating Microsoft Azure CSA, Dot Collective, Kumulus.
     - **Annotations / MRI-133** (`~/claude_code/projects/annotations`) - page identity & lineage; consider whether graph-based lineage ideas apply.
     - **LexVision PoC + Kumulus** (`~/claude_code/projects/lexvision-poc`) - ontology + rules + graph + classifiers; open ADR-002 (graph DB) and ADR-003 (NLP). See `docs/frontier-week-tech-learnings.md` already written there.
     - **Expert Sheet data processing** (`~/claude_code/projects/expert-sheet-data-processing`) - only if a genuine tie exists; do not force it.
     - Any other current work that genuinely connects.
   - Organise the digest as a flowing discussion (talk by talk, or theme by theme), calling out the standout product features and what Rowan should take from each for his projects. Aim for the depth that fills ~45 minutes of spoken audio (roughly 6,000-6,500 words of script).

2. **Render to audio via /work-digest.**
   - Use the /work-digest tool to produce the spoken audio in Rowan's voice / plain walking register. Note: /work-digest is built around session-log catch-ups, so this is a non-standard use - it is digesting *talk content*, not session activity. Either feed it the synthesised narration script, or use its rendering/voice stage directly; adapt as needed and keep its attended approval gate before writing/archiving any audio.

### Next steps
1. Run the per-project research/synthesis and present the structured analysis for Rowan's review.
2. On approval, assemble the ~45-minute narration script in his spoken register (UK English, no em dashes, plain language, no AI-speak).
3. Render to audio via /work-digest, pausing at its approval gate before archiving.

### Key references
- Meeting records: `~/claude_code/data_strategy/notes/frontier-week-{keynote-audio,data-silos,agentic-impact}-2026-06-22-meeting.md`
- Source graphs (summary.md, timeline.md, graph.html): `~/meeting-graph-output/frontier-week-*-2026-06-22/`
- LexVision tech slice already written: `~/claude_code/projects/lexvision-poc/docs/frontier-week-tech-learnings.md`
- Project hubs: `Projects/medbrief/MedBrief Data Strategy.md`, `Projects/lexvision/LexVision POC.md`
- Voice/register: `~/.claude/profile/writing-voice.md` and the /work-digest skill's spoken register.

### Notes for next session
- The three talks overlap heavily (Fabric IQ, ontologies, Foundry, agents, governance recur). Synthesise across them rather than repeating; the digest should feel like one coherent discussion, not three summaries.
- Rowan has not yet listened to or read the content himself, so the digest is his first real pass at it. Lead with what matters to his work.
- A model/effort note: this is synthesis-heavy; Opus / high or above suits it.
