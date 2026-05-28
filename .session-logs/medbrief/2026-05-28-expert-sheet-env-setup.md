---
date: 2026-05-28
project: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
domain: medbrief
session: Expert sheet dev env setup — venv, common_utils install, git init
type: wrap-up
tags: [expert-sheet, common_utils, azure-keyvault, pip, venv, git]
repos:
  - path: /Users/Rowan.Reid/claude_code/projects/expert-sheet-data-processing
    commit: ccd547b
---

## Session Summary

Picked up from the prior expert sheet orientation session. Retrieved the Gemini API key and PIP-URL from Azure Key Vault (`expertmarketplace-kv`), tracing PIP-URL's origin to a Confluence page by Fatima Rahman ("Azure artifact feed: common_utils package", page ID 1049657347). Created a Python venv at the project root, configured `~/.pip/pip.conf` globally with the private Azure Artifacts feed URL, and installed `common_utils` v0.2.1193 (the Confluence doc references v0.1.2 which no longer exists on the feed). Identified the most useful utilities for the task: `normalise_name` and `normalise_text` from `helper_textprocessing`, and `rapidfuzz` (installed as a dep) for Phase 2 fuzzy duplicate detection. Initialised the git repo with `.gitignore` correctly excluding `venv/`, `.env`, `*.xlsx`, and `.vscode/`. Environment is now fully set up; next step is building the Phase 1 classification script.
