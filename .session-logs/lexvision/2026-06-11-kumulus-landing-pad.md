---
date: 2026-06-11
domain: lexvision
type: handoff
parent:
tags: [kumulus, medbrief, landing-pad, deliverable]
---

# Kumulus Landing Pad working document

Built Rowan's own branded "Landing Pad" working document for the Kumulus/MedBrief engagement: a personal assembly surface he lifts content from into his shared doc for Deon and Laura. Added module-by-module Kumulus-vs-us cards, an entity-model section, a pseudonymisation ground-truth options brief, and a validated learning-primer companion; corrected a hallucinated benchmark ("Arcade") across the canonical docs.

## Continuation Prompt

## Continuation: Kumulus Landing Pad - introspective review + open decisions

**Parent session:** 2026-06-11-kumulus-landing-pad.md

### Context
Building Rowan's own branded working document, the "Landing Pad", for sharing with Deon and Laura on the Kumulus/MedBrief medico-legal engagement. It is a personal assembly surface: Rowan drives the real doc ("Rowan Output.docx") in Word and lifts content out of the Landing Pad.

### What was done this session
- Built `docs/kumulus/deliverables/Landing Pad.docx` from `landing-pad.spec.json` via a local `landing-pad-build.py` (branded docx builder: table / label_col / mono blocks, section page breaks, heading bookmarks; built locally because the medbrief-brand skill lacks these and editing it was blocked by the self-modification guard).
- Sections: technology table; module catalogue (M1-M12, three-column "Kumulus proposed vs we propose" cards with inputs/outputs/metric/benchmark/implementation, all external refs hyperlinked and verified); platform & infrastructure (I1-I7, longer write-ups, Laura's actual ask); architecture & cross-cutting (X1-X4); the entity model (patent-derived, ASCII hierarchy tree, value-vs-findability 2x2, Kumulus gaps as the agenda for Brendan's meeting); and the pseudonymisation ground-truth options brief (Label Studio etc., the South et al. caveat).
- Built `primers-and-further-learning.md`: a personal companion with validated, plain-English primers for ~60 referenced items (videos checked against transcripts via yt-dlp).
- Corrected the hallucinated "Arcade" benchmark across benchmarking.md, benchmarking-technical.md, and glossary.md (dropped in favour of Arize Phoenix / MLflow); left Brendan's source untouched.
- Rewrote the prose into Rowan's plainer first-person voice; removed all em dashes; narrowed margins; removed the TOC (Rowan will add it later in Word).

### Current state
- Project repo committed on main (55d9c63), not pushed (no push requested).
- Config repo (~/.claude) committed locally (4328517: profile voice update + central idea) but PUSH DEFERRED: a pre-existing cross-machine divergence causes rebase conflicts in learnings.md and memory-candidates.md (neither touched this session). Resolve per docs/MAINTENANCE.md before pushing; the local commit is safe.
- Vault: session log + memory backup committed and pushed.
- Note: settings.json working-tree model/effort values were reset to committed during the config rebase cleanup; re-run /model and /effort if the active selection looks wrong.

### Where we left off
The document is complete and builds cleanly. Two decisions were parked for a fresh session.

### Next steps
1. Introspective content review (the deferred task): sweep the whole Landing Pad and the dossier claims it rests on for anything else that does not do what we assumed, the way "Arcade" turned out not to. Check load-bearing benchmark/tool citations, capability claims, and figures.
2. Decide the Azure OpenAI primer link: keep the rebranded-but-live URL, or swap to the Foundry "what is" page (Microsoft folded the standalone "what is Azure OpenAI" page into Foundry).
3. Optional: the main doc says "TempReasoner for temporal ordering"; the paper is really about timeline construction. Tweak the wording if exact-match matters.
4. Resolve the ~/.claude cross-machine divergence and push the config commit.

### Key references
- Working doc: `docs/kumulus/deliverables/Landing Pad.docx` (+ `.spec.json`, `landing-pad-build.py`)
- Primer: `docs/kumulus/deliverables/primers-and-further-learning.md`
- Sources: `docs/kumulus/research/c5-entity-model.md`, `c7-annotation-tooling.md`, `05-patent-substantiation-map.md`, `benchmarking.md`
- People: Brendan Hughes (CEO, wants to meet Kumulus on the entity model), Deon Kuhn (CTO), Laura Gongas (AI lead, asked for the infra opinion + pseudonymisation ground-truth tooling)
