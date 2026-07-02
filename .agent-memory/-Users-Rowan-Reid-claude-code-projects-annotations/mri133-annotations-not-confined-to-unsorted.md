---
name: mri133-annotations-not-confined-to-unsorted
description: "Correction (2026-07-02, DB-confirmed) — annotated MedBrief documents are NOT confined to documents that bypassed DocSorter; a meaningful share are DocSorter-derived exports"
metadata: 
  node_type: memory
  type: project
  originSessionId: 62d479c6-b8dc-42c6-b2e0-b07d564b17c0
---

The June 2026 research (`docs/research/mri-133-research.md` §11) concluded annotation
"essentially does not happen" on DocSorter output, based on annotated documents having
zero `BatchDocument` link and almost none sitting in the `zzzz - Sorting Session Export`
collection. Deon corrected this directly (2026-07-02): annotated documents commonly HAVE
been through DocSorter. He's right — a code trace showed `SortingSessionExportPusher`
re-registers sorted output through the *same* generic archive-import service used for raw
uploads, so a sorted document loses its `BatchDocument` link on export and becomes
schema-identical to a never-sorted one. The June DB checks were measuring a signal
(`BatchDocument` link, current collection membership) that doesn't survive export, not
actual sort provenance.

Re-querying pre-staging with a creator+project+timestamp correlation (the one signal the
export path does leave: `Document.creator_id` = `SortingSession.exportPushBy_id`) found
**12.1% (668/5,536) to 25.4% (1,404/5,536)** of annotated documents plausibly DocSorter-
derived, spread across 445 distinct matters — not the "1 of 5,536" the June check found.

**Why:** changes the MRI-133 scope question from hypothetical to live. Annotation on
sorted-and-exported output is not a future workflow to plan for; it already happens today.

**How to apply:** do not cite mri-133-research.md §11's "annotation simply does not happen
[on sorted output]" claim without the 2026-07-02 addendum appended to that section. Full
methodology and the query approach are in the addendum itself (DB access via the pre-staging
tunnel documented in `~/claude_code/projects/expert-sheet-data-processing/docs/DB_TUNNEL.md`;
credentials for this project now live in this project's own gitignored `.env`).

**Propagated 2026-07-02** to every place the stale conclusion was load-bearing:
`docs/research/mri-133-research.md` §11 (the addendum) and §14 (new section, the export
mechanism this correction depends on), `docs/research/mri-133-divergent-
architectures.md` §8 ("the product fork" — was framed as a future either/or choice, now
correction notes both populations are already live), §9 (new ranked spike item 5), §10
(two open threads resolved/reversed), `docs/DESIGN-NOTES.md` (new 2026-07-02 dated entry),
`docs/OVERVIEW.md` (one-line summary corrected), `docs/IDEAS.md` (three new dated entries),
the vault decision `Decisions/2026-06-19-mri133-scope-and-stamp-first.md` (correction
section added; original Decision/Rationale left intact as the historical record), and the
branded export `output/MRI-133-research.{docx,spec.json}` (regenerated twice via
`~/.claude/skills/medbrief-brand/scripts/build_docx.py` + `md_to_spec.py`, most recently
after §14 was added). Deliberately NOT touched, per Rowan: Teams messages to Deon (already
discussed directly) and historical session logs (`.session-logs/medbrief/2026-06-18-*`,
`.session-logs/INDEX.md` line 27) — those stay as a record of what was concluded at the
time. See also [[mri133-content-arm-scoped-to-originals]] for the separate technical
finding (export mechanism, content-arm scoping) this same session produced.
