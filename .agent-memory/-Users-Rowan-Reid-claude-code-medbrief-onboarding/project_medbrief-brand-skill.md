---
name: medbrief-brand-skill
description: medbrief-brand skill builds branded docx/pptx from MedBrief brand tokens; palette decision (teal/green vs product indigo) still pending
metadata: 
  node_type: memory
  type: project
  originSessionId: 87fbc235-0c79-4746-b0b9-c128047bd13c
---

The **`medbrief-brand`** skill (`~/.claude/skills/medbrief-brand/`) generates
MedBrief-branded `.docx` and `.pptx` from brand tokens via python-pptx /
python-docx (self-contained venv via `scripts/setup.sh`). Built and visually
QA'd 2026-06-09. Research provenance: `notes/13-brand-design-system.md` in the
medbrief-onboarding project.

Tokens (canonical for external assets): primary teal **#009999**, accent green
**#72CC52** (the signature gradient), ink #1F2F3F; headings **Nunito Sans**,
body **Calibri** (Carlito-compatible). Logo assets bundled, incl. white
reversed variants for dark backgrounds (`scripts/make_white_logos.py`).

**Open decisions / gaps (the non-obvious part):**
- **Palette decision PENDING:** corporate teal/green vs the product React
  theme's indigo **#5E53D1** (the MedBrief Match "match" theme). Skill uses
  teal/green; flip one constant in `scripts/medbrief_tokens.py` to change.
- Type scale and logo clear-space are **inferred** (Confluence specs are
  images). To harden: get access to **GDES-174 "Templates"** (restricted) and
  the Drive/Figma brand masters.

Brand guidance source: Confluence space **GDES "MedBrief Design"** (microsite,
owner Adele van der Nest); archetype "The Magician". See [[ado-primary-code-host]].
