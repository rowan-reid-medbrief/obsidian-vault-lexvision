---
name: verify-structure-vs-usage
description: Don't infer usage from structure; verify load-bearing inferences against code/DB before building on them (MedBrief page-less case)
metadata:
  type: feedback
---

When reasoning about the MedBrief architecture, do not treat a structural property as evidence about usage. Concrete case (2026-06-19, MRI-133): I argued the drift problem was "largely hypothetical" because every annotated document is page-less, reading page-less as "never sorted". It is not. `Page` attaches to `BatchDocument` only, so every reviewable `Document` is page-less by design, sorted or not. Rowan caught it and asked me to double-check against the code, which overturned the inference.

**Why:** a confident reframe built on an unverified inference wasted a step and could have misdirected the work going to Dion.

**How to apply:** flag a load-bearing claim as inference versus verified fact, and verify it against the MSR code or the read-only DB before reasoning from it. See [[project_db-research-access]] for the DB route and [[project_medbrief-people]] for who owns what.
