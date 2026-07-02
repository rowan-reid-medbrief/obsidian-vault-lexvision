# Project Memory: Annotations (MRI-133)

- [MRI-133 project](mri-133-project.md): what this is, provenance (spun out of medbrief-onboarding), Deon/Rowan/PoC attribution, and the boundary against the other two medbrief hubs.
- [MRI-133 POC programme](project_programme_mri133-annotations-poc.md): POC runs as a tracked /programme; `/programme next` launches the next session.
- [Bake-off is clean-only](mri133-bakeoff-clean-only.md): the degraded (scanned) corpus variant is generated but never matched, so headline numbers are the easy-population best case.
- [venv path](mri133-venv-path.md): Python venv is at `poc/.venv`; Bash cwd resets each call, so use absolute paths.
- [Reporting & explanation prefs](reporting-explanation-prefs.md): show every %'s complement; plain framing; per-matcher "how it works"; Rowan often listens as audio.
- [Real-data container](mri133-real-data-container.md): Deon's Azure Blob container for real-case, non-synthetic MRI133 testing; structure + access notes.
- [Annotations not confined to unsorted docs](mri133-annotations-not-confined-to-unsorted.md): 12-25% of annotated docs are DocSorter exports, not "essentially never sorted" (June conclusion corrected 2026-07-02).
- [DB access for MRI-133 research](mri133-db-access.md): pre-staging jumpbox tunnel (port 3310); credentials in this project's own `.env`; production (3308) needs sign-off.
- [Content-arm should compare originals](mri133-content-arm-scoped-to-originals.md): match against never-repaginated `Page.pdfFile`, not exported bundles; also found the flatten-path stamp-destruction gap.
- [Stamp does not survive the real merge](mri133-stamp-not-survive-merge.md): spike (2026-07-02) proved a custom in-PDF page-dict stamp is LOST through PDFTron `PagePushBack` (not just flatten); use DB `Page.id`, not an in-PDF key.
- [Cardinality channels](mri133-cardinality-channels.md): SPLIT now PARTIALLY solved (token-space containment→set-cover→adjacency + geometric crop-residual resolve clean adjacent text splits; near-identical template + blank-page splits remain, need sequence-context / visual channel); pagination still fuses in for REMOVED/CLONE; degraded population collapses the content arm.
