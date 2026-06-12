---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
domain: medbrief
session: Advisory Q&A walking the Kumulus/Medbrief architecture for Rowan's "Rowan Kumulus Research" doc
type: wrap-up
tags: [kumulus, lexvision-poc, medbrief, architecture, cqrs, medallion, databricks, fabric, azure-ai-search, presidio, annotation-tooling, label-studio, advisory]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/lexvision-poc
    commit: 00a7003
---

## Session Summary

Advisory Q&A walking the Kumulus/Medbrief architecture module by module for Rowan's "Rowan Kumulus Research" doc. Established that CQRS was already in Kumulus's first (April) deck and is a scale-time serving pattern, not patent-mandated and rightly deferred for the PoV; that medallion is not patent-mandated either, with a two-zone Raw/Curated being the right-sized PoV form; and that the M2 (NLP semantic processing) / M3 (entity extraction) split is Rowan's own decomposition, since Kumulus bundled NLP into a single entity-detection step. Also covered the M2/M3 benchmarks, Fabric vs Databricks (why the engine moved to Databricks for unstructured medical data), Azure AI Search's evidence-retrieval role (M10), Presidio at scale and its text-not-PDF input (M1 OCR feeds it), and the pseudonymisation annotation-tooling comparison (Label Studio primary, INCEpTION runner-up, MedTator ruled out for the assisted workflow), all of which reproduced the dossier's existing position via background research workflows. Drafted two doc paragraphs (CQRS, medallion X2) for Rowan to paste manually, and logged the read-projection-output-contract idea to docs/IDEAS.md. Outstanding: verify the LegNER source and add a link in the M3 benchmark cell.
