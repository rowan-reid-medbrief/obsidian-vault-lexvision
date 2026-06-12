---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: medbrief
session: Captured ~15 of Rowan's writing-voice patterns from his own Landing Pad edits and applied them through the rest of the docx, then stripped patent and ADR reference numbers; doc renamed to Rowan Kumulus Research.docx
type: wrap-up
tags: [kumulus, medbrief, writing-voice, tone-pass, docx, profile, pseudonymisation]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
    commit: dbeec76
  - path: /Users/Rowan.Reid/.claude
    commit: f59e61b
---

Across several rounds, captured Rowan's writing voice from his own manual edits to the Kumulus working doc and added roughly fifteen patterns to `~/.claude/profile/writing-voice.md`: first-person action openers, purpose-as-bullets, strip stakes and meta-navigation, "Same as X" non-difference collapse, verdict effort-caveats, forward-phasing over rationale, casual "(I think?)" hedges, charitable-read-then-name-the-gap, gloss obscure tools even inside table cells, keep hedged decision-rationale while cutting significance, cut defensive disclaimers, strip invented precision, plus a named informal working-document register and the unifying "cut the framing, keep the decision and the concrete" principle; closing label standardised to "Summary."

Then applied that voice through the unedited sections of the docx: rewrote the M3-M12 benchmark cells from tag-shorthand to plain narration (hyperlinks preserved via `w:hyperlink` reconstruction), made four meta-navigation trims, removed all patent reference numbers (the Patent ref column plus ten heading parentheticals) and all ADR/decision-record references, reworded the M3 GLiNER cell (named the Foundry model; web-confirmed Foundry hosts Hugging Face models) and the M6 Presidio cell (now states Presidio does both finding and replacing), glossed REBEL, and fixed the M2 "unmaintained" typo. Mid-session the patent removal reverted once: first read as a Word save-conflict, but the build-venv memory notes a background process has silently rebuilt the old `Landing Pad.docx` from the stale spec before, the likelier cause. Rowan renamed `Landing Pad.docx` to `Rowan Kumulus Research.docx` (all edits confirmed present in the renamed file); the stale `Landing Pad copy.docx` was deleted and a generator-retirement idea logged.
