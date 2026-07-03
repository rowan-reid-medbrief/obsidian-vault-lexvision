# Project Memory: Annotations (MRI-133)

- [MRI-133 project](mri-133-project.md): what this is, provenance (spun out of medbrief-onboarding), Deon/Rowan/PoC attribution, and the boundary against the other two medbrief hubs.
- [MRI-133 POC programme](project_programme_mri133-annotations-poc.md): POC runs as a tracked /programme; `/programme next` launches the next session.
- [Bake-off populations](mri133-bakeoff-clean-only.md): both clean and degraded are now matched (`--population` flag); content-arm numbers are still the clean best case (quote degraded to Deon). Degraded OCR-collapse fixture bug fixed 2026-07-03.
- [venv path](mri133-venv-path.md): Python venv is at `poc/.venv`; Bash cwd resets each call, so use absolute paths.
- [Reporting & explanation prefs](reporting-explanation-prefs.md): show every %'s complement; plain framing; per-matcher "how it works"; Rowan often listens as audio.
- [Real-data container](mri133-real-data-container.md): Deon's Azure Blob container for real-case MRI133 testing; structure + access. **Corpus now 11 real docs local in `poc/data/real-samples/` (2026-07-03), all four provenances, incl. 2 real image-only docs + a 1344pp trust doc.**
- [Annotations not confined to unsorted docs](mri133-annotations-not-confined-to-unsorted.md): 12-25% of annotated docs are DocSorter exports, not "essentially never sorted" (June conclusion corrected 2026-07-02).
- [DB access for MRI-133 research](mri133-db-access.md): pre-staging jumpbox tunnel (port 3310); credentials in this project's own `.env`; production (3308) needs sign-off.
- [Content-arm should compare originals](mri133-content-arm-scoped-to-originals.md): match against never-repaginated `Page.pdfFile`, not exported bundles; also found the flatten-path stamp-destruction gap.
- [Stamp does not survive the real merge](mri133-stamp-not-survive-merge.md): spike (2026-07-02) proved a custom in-PDF page-dict stamp is LOST through PDFTron `PagePushBack` (not just flatten); use DB `Page.id`, not an in-PDF key.
- [Cardinality channels](mri133-cardinality-channels.md): SPLIT FULLY HANDLED (zero silent, both populations); **coverage-graph reframe DONE 2026-07-03** (`coverage_graph.py` IR overlay, `decide()` a shim, golden-fixture-proven output-neutral; the capacitated-solver backbone was dropped in hardening). Dormant REMOVED margin rule built but OFF pending corpus-expansion enable-gate. Pagination fuse still `[parked]`.
- [GitHub remote](mri133-github-remote.md): repo now has a private GitHub remote (`rowan-reid-medbrief/mri-133-annotations`, SSH via `~/.ssh/github`, `gh` installed) as of 2026-07-03; entire-hook also pushes its checkpoints branch.
