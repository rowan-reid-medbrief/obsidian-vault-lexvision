---
name: content-add-warranted-links
description: "When producing deliverable content, proactively hyperlink any term that warrants a link (benchmarks, tools, services, standards)"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 76df9006-4499-4271-8ae3-77d2b1a8ae6c
---

When creating content with Rowan (documents, the Kumulus landing pad, briefs), proactively add hyperlinks to any term that warrants one: named benchmarks, tools, services, standards, products. Use canonical/official sources where they exist; otherwise a reputable non-official source is fine. Where no good source exists, leave it plain and say so rather than inventing or mislabelling a link.

**Why:** Rowan reviews this material independently and wants to follow references straight to source. He asked for links to be the default, not something to be prompted for each time.

**How to apply:** In docx specs built via [[kumulus-landing-pad]], put links in the cell/paragraph `runs` arrays. In markdown docs, use standard `[text](url)` links. Verify load-bearing links rather than trusting recall (see the Arcade case: a real-sounding tool whose attributed capability did not exist). Related: [[kumulus-architecture-first-framing]].
