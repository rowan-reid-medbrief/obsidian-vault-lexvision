---
date: 2026-06-19
project: medbrief-onboarding
domain: medbrief
tags: [medbrief-brand, onboarding, de-identification, pptx, docx, skill-hardening, m365]
repos: [medbrief-onboarding, claude, ObsidianVault]
model_check: fired-downgrade-model
---

# Public onboarding pack + deck rebuild + brand-skill hardening

Built a de-identified, em-dash-free public version of the MedBrief onboarding pack (`medbrief-overview-public.{md,docx,spec.json}`) from `onboarding-pack-v1`: all individuals removed, external orgs (client firms, NHS Trusts, UCL) generalised, personal-onboarding framing stripped, ticket/Confluence IDs kept (per Rowan's scope choices). Rebuilt the knowledge-share deck through the upgraded medbrief-brand skill (Degular/Roboto), folding Rowan's hand-tuned font sizes into a 14pt PPTX body-text floor.

Hardened the skill's converter and docx builder so the pack rendered cleanly: `md_to_spec` now drops thematic breaks (`---`), folds wrapped list-item continuation lines into their item (fixed broken bullets and the §11 numbered lists), and parses inline markdown inside table cells; `build_docx` renders those cell runs and gives each numbered list its own start-overridden numbering instance so it restarts at 1. Removed all 47 em dashes from the pack (restructured, not hyphen-swapped). Also hit and recorded the cli-microsoft365 OneDrive file-download scope gap (browser-auth lacks Files scopes; 401/403/404 on spo file get + Graph /me/drive + /shares; use a download.aspx?UniqueId= link or yt-dlp+cookies).

Tests 47/47 (16 pptx + 31 docx); skills conformance 40/40 clean. Committed the 3 brand scripts to ~/.claude (pushed) and the deck + public pack to medbrief-onboarding (the Office `~$` temp lock file left out). Earlier in the session: pulled the edited deck from the user's personal OneDrive (m365 route blocked; user downloaded it), and diffed its hand-tuned fonts to derive the 14pt floor.
