---
name: feedback_code-walkthrough-audio-naming
description: "When narrating a spoken code walkthrough of a branch, name files explicitly alongside any ordinal, not ordinal-only"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 66d636c5-bb4f-436e-b171-01becc1eef5d
---

When producing an ad-hoc spoken "code walkthrough" audio digest of a branch's changes, reference each file by its actual name (class/interface name is fine, extension optional for spoken flow) in addition to any ordinal ("file one", "file two"), never ordinal-only.

**Why:** the first such walkthrough (the XOD branch, 2026-07-04) followed `work-digest`'s spoken-register rule that forbids reading file paths/names aloud (a rule tuned for the "catch-up on a walk" use case it was borrowed from). That made the digest hard to map back to the actual files afterwards. Rowan explicitly asked for names to be included on the second walkthrough (the PDF-split branch, 2026-07-07).

**How to apply:** this mechanism (rewrite doc-comments as narrative, hand-write a script, render via `work-digest`'s shared `render_audio.sh` helper) is bespoke, not a dedicated skill yet (tracked as a reflected idea, `~/.claude/docs/IDEAS.md` `#6y2ces`). Until that skill exists, override the ordinal-only spoken-register rule specifically for this narration type: say the class/interface name naturally (drop the file extension, it reads awkwardly aloud) alongside its ordinal position in the walkthrough.
