---
title: "Catch Up 2026-07-01 (meeting graph)"
type: note
created: "2026-07-01"
tags: [meeting-graph]
---

# Catch Up 2026-07-01

## TL;DR

[[Rowan Reid]] walked [[Deon Kuhn]] through a synthetic PDF test harness built to evaluate page-tracking approaches (exact hash, perceptual hash, text fingerprint, ensemble, and a metadata-stamped ID) for a document redaction and annotation product. The stamped-ID approach was clearly the strongest, but neither of them judged any of the approaches accurate enough for the accuracy bar the product needs. Deon spotted a second use for the research (duplicate/blank-page detection in record sorting) and proposed folding it into a product-marketing angle limited to sorted record sets. They agreed to test the approach on real records next, and Deon separately asked Rowan to research rendering a date-range-filtered subset of pages at scale in the Apprise viewer.

## Decisions

- Bundle the insight/redaction-retention benefits as a marketing proposition, limited to sorted record sets (tentative); decided by [[Deon Kuhn]]; insights and redaction-retention benefits both only apply to sorted record sets, so bundling them strengthens the product marketing angle.
- Test the matching approach on real (non-synthetic) records rather than only the synthetic dataset (made); decided by [[Rowan Reid]] and [[Deon Kuhn]].
- Implement redaction inside DocSorter at the sorting stage (tentative); decided by [[Deon Kuhn]]; clinicians are the people best placed to do the actual redaction in the first place. Alternative considered: a single unified solution attempting to solve redaction, annotation-attachment, and sorting all at once (Chantal's original ticket approach), which does not work and needs to be broken into separate solutions.

## Action items

- Speak to Chantal about limiting the sorted-set-only bundling/insights offering, owner: [[Deon Kuhn]].
- Test the matching approach on real (non-synthetic) records, owners: [[Rowan Reid]] and [[Deon Kuhn]].
- Locate the storage account containing real records for testing, owner: [[Deon Kuhn]].
- Research how to render a date-range-filtered subset of pages in the Apprise viewer (given the XOD format's incompatibility with byte-range requests) and test rendering performance at scale, owner: [[Rowan Reid]].

### Your follow-ups

- Research date-range filtered PDF rendering at scale in the Apprise viewer (personal commitment, from Deon's direct ask).

## Open questions

- "Is that when you discovered it?" (asked by [[Rowan Reid]]) — answered: yes, that was when Deon discovered his cat allergy.
- "How close is the text on the pages?" (asked by [[Rowan Reid]]) — answered: text_fingerprint compares textual similarity between pages.
- "Remember what I told you?" (asked by [[Deon Kuhn]]) — answered: Rowan confirms he remembers Deon predicting the approach wouldn't fully work.
- "How do you feel about all of this?" (asked by [[Deon Kuhn]]) — answered: Rowan found the research interesting and exciting, and was surprised the algorithms (especially perceptual hash) didn't perform as well as he'd expected.
- "Would solicitors still be able to redact by the time docs reach them, or no?" (asked by [[Rowan Reid]]) — answered: redaction is not currently available in the Apprise viewer (though relatively easy to add and much lighter than the old ShareBrief implementation); it's been in the backlog, and the market is trending toward automated rather than manual solicitor-driven redaction.
- "Can we stop recording?" (asked by [[Deon Kuhn]]) — OPEN (the captured recording ends here).

## Risks

- Because of the accuracy issues with the matching approaches, there is no margin for error in what they're working with (raised by [[Deon Kuhn]]).

## Artifacts referenced

- mri133 (tool) — the PDF page-matching test-harness CLI Rowan built.
- Apprise Viewer (product) — the PDF viewer used to apply annotations/redactions.
- annotations project (repo) — Rowan's local repo hosting the test harness.
- Pico PDF (tool) — used to stamp a unique metadata ID into PDF pages.
- bakeoff.html (document) — the visual bake-off report comparing matcher results.
- DocSorter (product) — where Deon proposes implementing redaction, at the sorting stage.
- ShareBrief viewer (product) — an older, more processing-heavy redaction viewer.
- XOD format (system) — incompatible with byte-range requests, forcing whole-PDF loading.
- Computer Electronic Records (dataset) — the one document type likely to reach very large page counts.
- SALLI (system) — MedBrief's sorting-algorithm system; its duplicate detection benefits from this matching research.

## People

- [[Rowan Reid]]: Engineer.
- [[Deon Kuhn]]: CTO.
- [[Lewis]]: Deon's partner, mentioned during a delivery interruption.
- [[Chantal]]: colleague Deon will speak to about the sorted-set-only bundling; her original ticket sought a single solution that turned out not to work.
- [[Lara]]: colleague expected to be interested in the research.
- [[Adam]]: CEO, prefers certain discussions not to be recorded.

## Graph views
![[graph.mermaid.md]]
