---
title: "Catch Up 2026-07-01 (timeline)"
type: note
created: "2026-07-01"
tags: [meeting-graph]
---

# Timeline: Catch Up 2026-07-01

## Chapter 1 — Personal catch-up: weekend and cat-sitting
**0:00 - 2:30**

Rowan and Deon catch up on their weekends before the technical discussion; Deon describes a cat-sitting trip near Cardiff and discovering a cat allergy.

Key lines:
- Deon: "We were house-sitting in an area just outside of Cardiff. So we're actually cat-sitting."
- Rowan: "And it was during that house-sitting that we both discovered that we are a little bit allergic to cats."
- Deon: "No, I tried to, as Lewis said, I sort of maybe loved the cat too much this weekend. And he ended up scratching me quite a bit."

## Chapter 2 — Screen share: synthetic PDF test harness walkthrough
**2:30 - 6:50**

*Rowan starts screen sharing in Microsoft Teams, showing VS Code with the 'annotations' project open in Explorer.*

Rowan shares his screen and walks Deon through the synthetic PDF/records generator, the resorting tool (deletes, inserts, rearranges, splits pages), and the page-matching engine that tracks what happened to each page.

Key lines:
- Rowan: "So basically, I generate PDFs, then I resort them. So I've got another command that does some resorting, which does a bunch of different things."
- Rowan: "And then I've got a matching engine, which uses different styles of matching to try and figure out what happened to each page."
- Deon: "As a quick note, when we ingest, obviously, the annotations, because they're in that format, the XFDF or whatever, we do, like, use the engine of Apprise to apply them to the pages."

## Chapter 3 — Running the end-to-end matcher; delivery interruption
**6:50 - 13:20**

*Continued screen share of VS Code, Explorer sidebar showing the annotations project's top-level files.*

Rowan kicks off the full end-to-end MRI133 run across all matchers. Deon is interrupted by a delivery requiring his physical presence (his partner Lewis is mentioned) and steps away briefly before returning.

Key lines:
- Rowan: "So, if I go MRI133, this actually runs it end-to-end and runs each matcher."
- Deon: "Rowan, can I go get the delivery quick? Sorry. Because they need to see my face. It's not a one that they can pick up."

## Chapter 4 — Reviewing matcher results and the stamped-ID approach
**13:20 - 18:13**

*VS Code with a PDF page viewer behind a terminal showing the output of `./mri133 run --matchers all`, comparing matching approaches.*

Rowan explains the matching algorithms (exact hash, perceptual hash, text comparison, ensemble) and their precision/recall/silent-error tradeoffs. The metadata-stamped page ID approach is by far the most reliable, failing only on true duplicates or unlinked splits.

Key lines:
- Rowan: "Of those that it was confident about, it got 92.9% right, which is good, right?"
- Rowan: "So anyway, it's really bad at split. So actually, if a page has been split, it basically thinks the page is gone."
- Rowan: "The stamped route is by far and above, like, it gets rid of all the crazy noise and trying to figure out, like, how to do the right matching."
- Deon: "I mean, I like the stamp, but none of these, to my eye or to my, like, sort of reasoning, are accurate enough."

## Chapter 5 — Implications: duplicate detection reuse and product bundling
**18:13 - 21:22**

*Browser-rendered bakeoff.html report, bar charts breaking down precision, recall, and abstention judgement for each matcher.*

Deon realises Rowan's work also solves duplicate/blank-page detection for the record-sorting algorithm (relevant to SALLI, MedBrief's sorting system, and to Chantal's work), all without an LLM. He proposes bundling insight/redaction guarantees as a marketing angle limited to sorted record sets.

Key lines:
- Deon: "Do you know what you've actually done now is you've solved another problem we have, which is duplicate detection in the sorting algorithm for Sally [SALLI]."
- Deon: "And Lara would be very interested in all of this, because this is fascinating. ... This is all deterministic methodology."
- Deon: "Much of the insights also only applies to sorted sets of records. So we can bundle it as a marketing thing."

## Chapter 6 — Reflection and proposal to test on real data
**21:22 - 23:07**

*Split-screen webcam view of Rowan and Deon talking after the screen share.*

Both reflect on the results being less accurate than hoped despite deterministic hashing methods. They agree to try the approach against real (not synthetic) records, with Deon offering to locate the storage account.

Key lines:
- Rowan: "I thought that it would do better than it did."
- Deon: "I actually had high hopes for this. ... But I guess it's just not."
- Deon: "You can try it as an extension of the research because I don't think it will go to waste. I'll find the storage account quickly."

## Chapter 7 — Redaction workflow and DocSorter placement
**23:07 - 25:09**

Deon explains that redaction should live in DocSorter at the sorting stage, since clinicians are best placed to redact. The current Apprise viewer lacks redaction; the market is trending toward automated redaction rather than manual solicitor workflows.

Key lines:
- Rowan: "So, would, like, solicitors and them be able to still redact when they get, by the time the docs get to them, or no?"
- Deon: "Redaction is currently not available inside the appraise viewer that we have. It is relatively easy to do, to be honest."
- Deon: "The market is gearing towards automated redaction. ... Solicitors, like, don't really want to go and, like, have to do that."

## Chapter 8 — New research ask: date-range filtering and PDF rendering at scale
**25:09 - 27:42**

Deon asks Rowan to research how to render a date-range-filtered subset of pages in the Apprise viewer, given the XOD format's incompatibility with byte-range requests, and to test performance against very large PDFs.

Key lines:
- Deon: "It's not compatible with the format that we use with the XOD because that uses byte range requests, and it only renders the pages that you're viewing."
- Deon: "I do have another little bit of research I want you to do if you have time."
- Rowan: "I mean, I can easily generate some fat PDFs and see what happens, yeah."

## Chapter 9 — Wrap-up: CEO's recording preference
**27:42 - 28:02**

Deon raises an off-topic point about Adam (CEO) preferring not to record certain discussions, and asks to stop recording, ending the captured portion of the meeting.

Key lines:
- Deon: "So Adam has been, Adam as CEO is very heavy on, can we stop recording?"
