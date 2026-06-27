---
date: 2026-06-27
project: /Users/Rowan.Reid/claude_code/projects/annotations
domain: medbrief
session: MRI-133 narrated demo MP4 + reusable demo-walkthrough image/artefact capability + a fail-closed export contract
type: wrap-up
tags: [annotations, mri-133, demo-walkthrough, poc, deon-demo, piper]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/annotations
    commit: 69f6099
  - path: /Users/Rowan.Reid/.claude
    commit: 2bb6c6d
model_check: not-needed
---

## Session Summary

Built the narrated MP4 walkthrough of the MRI-133 PoC for Deon (4:06, piper voice, concept diagrams with node-tracking box highlights, and before/after burn-vs-abstain proof frames), then made it reproducible from tracked assets. MRI-133 gained `mri133 demo --all --export` (fail-closed: copies curated pii_safe before/after pages plus a `.demo-artefacts.json` contract into a committed `demo-assets/`, refusing any keyless or non-cross-checked run), and the demo-walkthrough skill gained a reusable image/compare/`artefact_surfaces` capability so a no-UI artefact-emitting CLI can hand its rendered outputs to image beats without `--allow-no-contract`. Proved the contract path renders byte-identical to the pre-contract bypass (C+E visually inert); the v7 MP4 plays in QuickTime (AVFoundation oracle stddev 29.11) and `deliver.py` dry-run is clean. 215 poc tests green (+14 export); annotations committed to local `main` (69f6099, no remote), ~/.claude committed + pushed (2bb6c6d).
