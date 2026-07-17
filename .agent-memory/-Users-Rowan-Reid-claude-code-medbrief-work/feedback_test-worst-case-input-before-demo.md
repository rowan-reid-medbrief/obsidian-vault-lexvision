---
name: test-worst-case-input-before-demo
description: "When demoing a document/data-processing pipeline's quality to stakeholders, test the actual representative worst-case input, not just the clean/convenient one to build"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 459fab8f-cbf0-4ee2-9931-2eac50d7756d
---

Test the input shape the real use case actually has, not the easiest one to construct, before presenting quality findings to stakeholders.

**Why:** during the AI-2066 translation demo (2026-07-17), the first test used clean digital text because it was quick to synthesise. That test alone would have overstated confidence: on rerun against a rasterised, scanned-style variant (the actual shape of the real ticket sample, case 44240 — 43 pages of scanned images), the quality problem reversed. A sentence that silently vanished on the clean-text path was present on the scanned path, which instead showed a different set of visible defects. Caught via an `advisor()` call before presenting, not by my own first-pass plan — testing only the convenient input shape was the blind spot, not something I'd have flagged unprompted.

**How to apply:** before showing anyone a "here's the quality" result for a pipeline whose real input has a specific shape (scanned vs digital, messy vs clean, large vs small), check whether the test input matches that shape. If it's cheap to also test the harder/more-representative shape (as it was here — a rasterise step), do it before the demo, not after someone asks "but what about the real documents." Applies beyond MedBrief: any demo of an OCR, extraction, translation, or data-quality pipeline where the built test fixture is easier to make than the real thing.
