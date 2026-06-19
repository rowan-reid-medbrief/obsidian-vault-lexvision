---
name: medbrief-brand-skill
description: medbrief-brand skill builds branded docx/pptx from MedBrief brand tokens; palette + fonts now confirmed against the official design system (design.medbrief.co.uk)
metadata: 
  node_type: memory
  type: project
  originSessionId: 87fbc235-0c79-4746-b0b9-c128047bd13c
---

The **`medbrief-brand`** skill (`~/.claude/skills/medbrief-brand/`) generates
MedBrief-branded `.docx` and `.pptx` from brand tokens via python-pptx /
python-docx (self-contained venv via `scripts/setup.sh`). Built 2026-06-09;
**tokens confirmed against the official public design system at
https://design.medbrief.co.uk on 2026-06-19** (supersedes the earlier
image-only Confluence guidance and `notes/13-brand-design-system.md`).

Palette (canonical for external assets): a three-accent system over warm
neutrals. Primary teal **#009999**, Secondary green **#72CC52** (the signature
gradient), Tertiary indigo **#5E53D1**; each with a tint. Neutrals: background
#F7F5F2, dark background #030029, headings #141413, body #403F3E. Headings
**Degular** (Adobe Fonts, 3 desktop seats, marketing-only, falls back when not
installed), body **Roboto** (open source, Arial email fallback). Logo assets
bundled, incl. white reversed variants for dark backgrounds.

**Resolved since the v1 build (the non-obvious part):**
- **Palette decision RESOLVED:** indigo #5E53D1 is the official **Tertiary**
  accent, not a product-only colour. Teal stays primary for external assets;
  indigo is now the `TERTIARY` token. (Earlier note had this "pending".)
- **Fonts corrected:** were Nunito Sans / Calibri (inferred); now Degular /
  Roboto (confirmed).
- **`INK` token deprecated:** the old single #1F2F3F did double duty as dark
  fill and dark text. Now split into `DARK_BG` / `BODY_TEXT` / `HEADING_TEXT`;
  `INK` kept as an alias to `BODY_TEXT`.
- Type scale and logo clear-space are now **confirmed** (were inferred).

**Remaining gaps:** exact shape corner-radius px, elevation CSS values,
gradient stop values, logo minimum size, and official Office/Figma masters
(the design site's `/resources` download area was not reachable from the CLI).

See [[ado-primary-code-host]].
