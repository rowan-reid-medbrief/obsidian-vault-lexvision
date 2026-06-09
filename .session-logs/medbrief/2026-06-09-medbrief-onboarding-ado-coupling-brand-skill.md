---
date: 2026-06-09
project: /Users/Rowan.Reid/claude_code/medbrief-onboarding
domain: medbrief
session: ADO 12-repo discovery + correction, vault coupling, and the medbrief-brand docx/pptx skill
type: wrap-up
tags: [medbrief-onboarding, azure-devops, vault-coupling, brand, design-system, medbrief-brand, skill-creation, confluence]
repos:
  - path: /Users/Rowan.Reid/claude_code/medbrief-onboarding
    commit: f304ded
---

## Session Summary

Discovered that MedBrief's Azure DevOps (`MedBrief AI`) hosts 12 active git repos - the AI team's primary code host - correcting earlier onboarding notes that assumed Bitbucket-only; fixed notes/00,07,08 and saved a memory. Promoted medbrief-onboarding to a vault-coupled project (CLAUDE.md coupling section, docs/SOURCES.md up-link, a curator-written hub note, and an entry on the Coupled list in KNOWLEDGE-ARCHITECTURE.md). Interrogated Confluence (GDES "MedBrief Design"), Jira and the app codebase for brand guidance and built the `medbrief-brand` skill (branded docx/pptx via python-pptx/docx, teal #009999 / green #72CC52 tokens, bundled logos incl. white reversed variants) plus notes/13 research; visually QA'd via a newly-installed LibreOffice (which caught a low-contrast cover logo and a YAML conformance bug, both fixed). Open: the brand palette decision (teal/green vs product indigo) and access to GDES-174 + Drive brand masters.
