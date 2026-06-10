---
date: 2026-06-10
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: medbrief
session: Assessed Kumulus's revised (gen 3) proposal, appended ADR-008, re-baselined the dossier, ran a 206-agent corpus audit and applied 69 verified fixes
type: handoff
tags: [kumulus, medbrief, revised-proposal, adr-008, corpus-audit, workflow-orchestration, citations, benchmarking]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
    commit: two wrap-up commits (see git log; pre-session HEAD adc7386)
---

## Session Summary

Kumulus's revised zero-cost proposal arrived with the scope split inverted (they keep the comparison layer; MedBrief owns the prep zone), and the session produced the assessment of record (doc 10, with the three-generation evolution trace), ADR-008 (accept in principle, eight gating conditions), and the Stream 3 response brief for Laura and Deon. A 206-agent ultracode corpus audit over the 28-file dossier then confirmed 69 findings, all applied: dossier re-baseline propagation, a wrong CausalBench arXiv ID in four files, the 57.6% figure re-attributed in the canonical benchmarking docs, dead links, and a jumpbox-command redaction. Next: tone pass, regenerate both branded docx, send, and pick the meeting slot.

## Continuation Prompt

## Continuation: Kumulus deliverable polish and send

**Parent session:** 2026-06-10-kumulus-revised-proposal-assessment-and-corpus-audit.md

### Context
LexVision POC, Kumulus engagement. Kumulus's revised zero-cost proposal (received 10 June) inverted the scope split: they keep the comparison layer (NICE, Databricks, data contract validation, explainable outputs) and MedBrief owns the prep zone. The position is ADR-008: accept in principle, negotiate eight gating conditions. The deliverables for Laura and Deon are written but not yet polished or sent, and Joao offered meeting slots on 11 June 16:00 or 15 June 15:00 (Dublin).

### What was done this session
- Assessed the revised proposal with a three-generation evolution trace: `docs/kumulus/10-revised-proposal-2026-06-10.md` (the GBP 0 is engineered to the penny against two Microsoft incentives and is conditional on their approval; the 2020 NICE version rests on the National Archive route, not the API).
- Appended ADR-008 (accept in principle, eight gating conditions) plus an ADR-006 erratum (Presidio figure misattribution).
- Re-baselined the dossier with dated revision notes; wrote the Stream 3 response brief (`deliverables/stream3-revised-proposal-response.md` + branded docx).
- Ran a 206-agent corpus audit (7 dimensions, two-lens adversarial verification): 69 findings confirmed and all applied, including the wrong CausalBench arXiv ID in four files and the 57.6% Qwen3-32B re-attribution to arXiv:2510.07231v1 in `docs/benchmarking.md`, `docs/benchmarking-technical.md`, and the glossary. Report: `docs/kumulus/audit-2026-06-10.md`.
- Recorded Rowan's framing as project memory: the modular architecture (modules, build approach, benchmarks per module) is the primary artefact; which side builds each module is fluid and secondary. Frame dossier questions as owner-fluid, never "superseded because the vendor split changed".

### Current state
All committed: project commits `ef62d13` + `71b6209`, vault pushed. Both ADR-007 and ADR-008 sit at Proposed pending team alignment. `stream1-laura-asks.docx` is STALE against its corrected markdown; `stream3-revised-proposal-response.docx` matches its markdown but predates the tone pass.

### Where we left off
Rowan flagged the Stream 3 register as not his tone (specific phrases: "the marquee feature", "contingent liability", "prepared-case production line", "keeps the momentum", "sized by money") and deferred the rewrite. Both docx files need regenerating after it.

### Next steps
1. Tone pass on `stream3-revised-proposal-response.md` with Rowan, replacing the flagged phrases (read `~/.claude/profile/writing-voice.md` first).
2. Regenerate both docx files via the medbrief-brand builder (stream1 spec needs the images and hyperlinks; note the builder lacks bold/numbered lists, see learnings 58).
3. Send to Laura and Deon and choose the meeting slot (Brendan's non-UK compliance answer favours 15 June).
4. Chase the named residuals: Deon (OCR layout, PII detector intent, old daily ETL), NICE in writing (action:0002, now on the PoV critical path), Agilio (CKS, likely out of PoV scope).
5. Stand up the prepared-case production line (ADR-005 Presidio de-id, Label Studio per c7, ground truth per Laura's priority); it gates the PoV and doubles as the evaluation dataset.

### Key references
`docs/kumulus/10-revised-proposal-2026-06-10.md` (assessment of record); `docs/kumulus/audit-2026-06-10.md`; `docs/decisions.md` (ADR-008, erratum); `deliverables/stream3-revised-proposal-response.md`; the proposal PDF and covering email in `source_material/kumulus/`; backlog ideas in `docs/IDEAS.md`.

### Notes for next session
- learnings.md entry #56 | skill | workflow-orchestration | composability | Workflow args arrive as a JSON string; parse defensively.
- learnings.md entry #57 | skill | workflow-orchestration | output | null verifier results must not be counted as verdicts.
- learnings.md entry #58 | skill | medbrief-brand | scope | docx builder lacks bold and numbered-list support.
