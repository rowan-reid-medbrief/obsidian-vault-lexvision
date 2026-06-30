---
date: 2026-06-29
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: MedBrief-branded hands-on walkthrough for the MRI-133 PoC, plus a ./mri133 launcher and a resort step
type: wrap-up
tags: [mri-133, annotations, medbrief-brand, demo, poc, deon, walkthrough]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: beb3a4d
model_check: not-needed
---

## Session Summary

Built a MedBrief-branded hands-on walkthrough (`output/MRI-133-PoC-Walkthrough.docx`, from `docs/poc-walkthrough.md`) that steps Rowan through demoing the MRI-133 PoC to Deon: the bake-off measurement (generate, re-sort, score) and the visual redaction-safety demo, both verified to run today (the Apryse key still burns; the cross-check passes). To make it demoable beat by beat, added a `./mri133` launcher (loads `.env` + venv, no activation) and a new `mri133 resort` verb that re-sorts the documents as its own step before scoring, sharing the bake-off's mutation path (`mutate_under_scenario`) so what is shown is exactly what is scored. 207 poc tests green; recorded a learnings note on the medbrief-brand markdown converter.
