---
title: "Deon, Laura, Rowan: NICE guidelines and AI-2066 (meeting graph)"
type: note
created: "2026-07-17"
tags: [meeting-graph]
---

# Deon, Laura, Rowan: NICE guidelines and AI-2066

> Source: narrated recollection, not a recording. Rowan dictated this shortly after an unrecorded meeting. Treat detail as paraphrase, not verbatim quotation.

## TL;DR

Two topics. On the Lexvision POC's Kumulus project, Laura asked [[Rowan Reid]] to find which NICE guideline versions the Kumulus case set actually needs (checking clinical summaries, chronologies, and ECAs in MedBrief), then check whether those versions are reachable through the new NICE API trial, which currently only exposes current guidelines. If not, the task extends to a scraping/extraction proof of concept, with [[Deon Kuhn]] ruling out storing guidelines on the MedBrief server itself. On AI-2066, [[Rowan Reid]] got sign-off to use his own blob storage and to upload the real PHI sample, but showed [[Deon Kuhn]] and [[Laura Gongas]] three translation defects from the digital-path demo test, prompting an agreement to benchmark other translation services before touching real PHI.

## Decisions

- NICE guidelines should not be stored on the MedBrief server; needs a separate store aligned with the broader data strategy (tentative); decided by [[Deon Kuhn]]; not needed for the POC itself, only for eventual production.
- Approved the blob storage Rowan created under the MedBrief Secure Review subscription for AI-2066 translation testing, rather than any storage Laura may already have had attached from her own prior testing; decided by [[Deon Kuhn]], [[Laura Gongas]].
- Approved uploading the real PII-bearing German record for translation testing; decided by [[Deon Kuhn]], [[Laura Gongas]].
- Agreed to benchmark clinicalrecord-translator by extracting the German pages from the real sample document, translating them, and comparing the output against the English pages already embedded in the same document as ground truth (proposed, not yet executed); decided by [[Rowan Reid]], [[Deon Kuhn]], [[Laura Gongas]].
- Agreed next step: benchmark other translation services (AWS, Google, DeepL) on synthetic documents first, and only move to real PHI through whichever service shows better results; decided by [[Rowan Reid]], [[Deon Kuhn]], [[Laura Gongas]].

## Action items

- Go into MedBrief, find the specific cases supplied to Kumulus, and check their clinical summaries, chronologies, and ECAs to identify which NICE guideline version(s) are actually referenced or applicable per case, owner: [[Rowan Reid]].
- Check whether those specific NICE guideline versions are available via the NICE API, owner: [[Rowan Reid]].
- If not available via the API: investigate scraping or another extraction route, then store the guidelines locally as a proof of concept, owner: [[Rowan Reid]].
- Design a longer-term strategy, such as a cron job, to keep guidelines current, secondary to proving technical feasibility, owner: [[Rowan Reid]].
- Extract the German pages from the real sample document, run them through clinicalrecord-translator, and compare against the embedded English ground truth, owner: unassigned.
- Benchmark other translation services (AWS, Google, DeepL) on synthetic documents first, owner: unassigned.

### Your follow-ups

- Go into MedBrief, find the specific cases supplied to Kumulus, and check their clinical summaries, chronologies, and ECAs to identify which NICE guideline version(s) are actually referenced or applicable per case.
- Check whether those specific NICE guideline versions are available via the NICE API.
- If not available via the API: investigate scraping or another extraction route, then store the guidelines locally as a proof of concept.
- Design a longer-term strategy, such as a cron job, to keep guidelines current (secondary priority).

## Open questions

- Whether the NICE guideline versions actually needed for the Kumulus case set are obtainable, given the API's six-month trial appears to expose only current versions and the Kumulus cases may reference older ones (asked by [[Laura Gongas]]) OPEN.
- Whether the NICE guideline link found in an unrelated case's clinical summary reflects a clinician actively citing the guideline, or is just part of a generic appendix that happened to reference NICE content (asked by [[Laura Gongas]]) OPEN.
- Why the NICE guideline link did not load when Rowan clicked it (asked by [[Rowan Reid]]) OPEN.
- Whether uploading the real PII-bearing German record was okay (asked by [[Rowan Reid]]): Yes, both Deon and Laura approved it.

## Risks

- NICE guideline terms and conditions and licensing need consideration before guidelines can be extracted or stored; not resolved on the call (raised by [[Rowan Reid]]).
- Pseudonymisation testing has not been working well (raised by [[Laura Gongas]]).

## Artifacts referenced

- NICE guidelines (dataset)
- NICE API (tool)
- Kumulus case set (dataset)
- MedBrief (system)
- Data Lake (system)
- Databricks (system)
- SQL Server (system)
- Blob storage, AI-2066 / clinicalrecord-translator (system)
- MedBrief Secure Review subscription (system)
- clinicalrecord-translator (product)
- Real sample document, transposed German/English, PII-bearing (document)
- Digital, non-scanned demo test document (document)
- AWS (product)
- Google (product)
- DeepL (product)

## People

- [[Rowan Reid]]: narrator of this recollection.
- [[Deon Kuhn]]: CTO, MedBrief.
- [[Laura Gongas]]

## Graph views

![[graph.mermaid.md]]
