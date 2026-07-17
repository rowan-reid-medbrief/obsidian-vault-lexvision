---
title: "Deon, Laura, Rowan: NICE guidelines and AI-2066 (timeline)"
type: note
created: "2026-07-17"
tags: [meeting-graph]
---

# Timeline

> Source: narrated recollection, not a recording. There is no real audio timeline; segment positions below are nominal ordering within the narration, not elapsed minutes.

## Chapter 1: NICE guidelines for the Lexvision POC Kumulus project

Segments 0-12 (nominal).

Laura asked Rowan to check which NICE guideline versions the Kumulus case set actually needs, whether they're reachable via the new (current-only) NICE API trial, and if not, to look into scraping and local storage as a proof of concept. Deon ruled out storing guidelines on the MedBrief server. An unresolved incident: Laura found a NICE guideline link in an unrelated case's clinical summary, of disputed relevance, that Rowan couldn't open.

Key lines:
- "Ask (Laura to Rowan): investigate whether the NICE guidelines actually needed for the Kumulus case set are obtainable... the Kumulus cases may reference older versions."
- "Deon said guidelines should not be stored on the MedBrief server. Needs a separate store, likely aligned with the broader data strategy."
- "Laura found a clinical summary on a case (not one of the actual Kumulus cases) containing a link to a NICE guideline... The link itself did not load for Rowan when clicked."

No representative screenshot (narration has no recorded visual layer).

## Chapter 2: AI-2066 translation project update

Segments 13-22 (nominal).

Rowan showed Deon and Laura his own blob storage and the digital-path demo translation defects (untranslated banner, dropped diagnosis sentence, lost signature line breaks). New context surfaced: the real PHI sample is a transposed German/English document, suggesting a built-in benchmark. Agreed next step: test other translation services on synthetic data before touching real PHI.

Key lines:
- "Rowan demonstrated the blob storage he had created under the MedBrief Secure Review subscription. Deon and Laura were fine with it."
- "The real sample document is not purely German. It is transposed German and English, alternating a few pages of German with the English translation of those same pages."
- "Problems shown: the red header banner did not get translated into English; a sentence was missing under the Diagnosis section... the signature block at the bottom lost all its line breaks."
- "Agreed next step: benchmark other services (AWS, Google, DeepL) on synthetic documents first."

No representative screenshot (narration has no recorded visual layer).
