---
name: feedback_code-comment-tone-review
description: "When reviewing code comments in this repo for tone, check word choice against the writing-voice AI-speak list too, not just structural tells"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 92040f00-896d-4b96-a840-4e6c92fa7a99
---

Code comment tone review in this repo needs to check word choice against `~/.claude/profile/writing-voice.md` (the cross-machine AI-speak avoid-list and plain-language preference), not only structural patterns like ticket self-references, meta-navigation ("read this file first"), or filler adverbs ("deliberately"/"strategically").

**Why:** Asked for a tone pass on the MRI-134 branch's new/changed comments (2026-07-09). A first pass caught the structural tells cleanly but missed a plain vocabulary mismatch: "conflated" in a controller docblock. Rowan flagged it directly: "words like conflate... not words that I would use" — phrasing that names a category (elevated/academic-register words with a plainer everyday equivalent), not a single one-off.

**How to apply:** When reviewing code comments for tone, scan text that structural checks would call "clean" for the same category of issue writing-voice.md targets in prose: elevated/academic vocabulary, editorial framing, meta-narration. Don't assume a word is fine just because it's technically precise — "materialise/materialised" was checked in the same pass and left alone as legitimate domain terminology (cf. "materialised view"), not padding. The bar is "a word Rowan would actually say," which is narrower than "technically correct" and different from "not an obvious AI-speak marker."

Also confirmed: he wants strong class/method-level docblocks paired with more, not fewer, brief inline comments on non-obvious lines — e.g. why a validation check exists in two places, or why a specific test input was chosen. Terseness at the structural/framing level (no ticket refs, no meta-navigation) does not mean under-commenting the fiddly bits of the actual logic.
