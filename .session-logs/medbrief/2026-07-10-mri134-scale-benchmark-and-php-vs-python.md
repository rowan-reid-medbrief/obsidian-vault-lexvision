---
type: handoff
date: 2026-07-10
domain: medbrief
project: medbrief-work
ticket: MRI-134
parent: 2026-07-10-medbrief-work-docs-reorg-and-vault-alignment.md
tags: [medbrief, mri-134, benchmark, pdfnet, performance]
---

# MRI-134 scale benchmark, check-order fix, and PHP-vs-Python

Benchmarked the page-subset pipeline for Deon (where does the limit lie, is it pages or file size), fixed a check-order bug, then answered Deon's Python follow-up. The standalone-PHP control (Rowan's idea) overturned the conclusion: the real cost is a ~19x overhead inside the MedBrief runtime, not the language or engine. Next: profile that path to find the culprit.

## Continuation Prompt

## Continuation: MRI-134 profile the MedBrief runtime overhead

**Parent session:** 2026-07-10-mri134-scale-benchmark-and-php-vs-python.md

### Context
MRI-134 (date-range page filtering in MedBrief's Apryse viewer). Deon stress-tested the page-subset endpoint (a 13,000-page/5GB document timed out); this session benchmarked where the cost lies, fixed a check-order bug, and answered Deon's "would Python be faster?" follow-up. The benchmark work runs against the real pipeline on the dev VM (rowan-dev, container `docker-php-1`).

### What was done this session
- Reproduced the failure on the VM with synthetic PII-free fixtures (1k-13k pages). Answer to Deon: two stacked costs, copying the file scales with size, slicing scales with page count. Not an OOM here; the failure mode is "slow". Source fields are local disk, not Azure, so the real download is unmeasured.
- Fixed a check-order bug: the page cap was validated only after the full copy + open, so an over-cap request paid ~15s before rejection (Deon's exact experience). Split `PageSpecParser` into `parseSpec` (source-independent syntax+cap) and `assertWithinPageCount` (needs page count); controller calls the early gate before the copy. Now instant. 17 tests green.
- Answered the Python follow-up, and Rowan's standalone-PHP control overturned it: standalone external PHP (direct PDFNet, no Symfony) is the fastest of everything, 12-22x faster than the same op through MedBrief, and beats standalone Python. So the cost is NOT the language or engine version: it is a ~19x overhead inside the MedBrief runtime, on the page-insert step. Ruled out: language, engine version, xdebug, dev/prod, error handlers, GC/heap, SetTempPath, autoloader. Remaining: the booted Symfony kernel/DI container.
- Built a screen-share visual (real data), demoed to Deon, who was happy.

### Current state
- Workspace `medbrief-work` on `main`, commit 7d770d0 (pushed): DESIGN-NOTES, OVERVIEW, IDEAS updated.
- Vault committed + pushed (session log, Next Up).
- Repo `repo/` on `feature/MRI-134-pdf-split-approach`: the check-order fix is UNCOMMITTED (`ProjectDocumentController.php`, `PageSpecParser.php`) - wants review before commit. `Mri134BenchCommand.php` is present but guarded out of the product repo via `.git/info/exclude` (do not commit).
- Meeting visual: https://claude.ai/code/artifact/b640ad96-d921-47ad-bb4b-c837f41618a1

### Where we left off
Rowan chose to go the profiler route to find the ~19x overhead. Nothing started on it yet.

### Next steps
1. **Profile the MedBrief extraction path** (Xdebug profile mode / callgrind, or Blackfire) to name the exact culprit in the booted kernel that slows PDFNet's page-insert ~19x. Standalone `phpbench.php` (fast) vs the `bin/console app:mri134-bench --breakdown` path (slow) is the A/B; both on the VM.
2. Review the uncommitted check-order fix, then commit it (or ask Rowan first, per his standing preference).
3. Remove the stray malformed benchmark comment in `repo/src/Service/PDFTools/Split/PDFTronSplitPdf.php` (mid-method, not intentional).
4. Clean up the VM: ~26GB throwaway fixtures + harnesses in the `docker-php-1` container at `/var/tmp/mri134/`, and the `PyMuPDF`/`apryse-sdk` libs installed in `/opt/venv`. Command: `docker exec docker-php-1 rm -rf /var/tmp/mri134`.
5. (Optional, low value now) Matched-version tests: 11.4 Python needs a fresh Apryse trial key from Deon's account; 12.0 PHP needs the extension installed side-by-side in the container.
6. Still the real feature blocker: Workstream B, date-range -> per-document page mapping via `ChronologyItem` Bates refs.

### Key references
- `~/claude_code/medbrief-work/docs/mri-134/DESIGN-NOTES.md` - 2026-07-10 entry: full tables, the internal breakdown, the elimination table, the PHP-vs-Python and standalone findings, the matched-version status.
- Harnesses on the VM: `/var/tmp/mri134/phpbench.php` (standalone PHP, diagnostic toggles ERRH/HEAP/GC/TMPPATH/AUTOLOAD), `/var/tmp/mri134/pybench.py` (apryse/pymupdf). Copies in the session scratchpad.
- The demo PDFNet key is `pdftron_sdk_license_key` in `repo/config/parameters.yaml` (a per-platform PHP trial key).
- VM: `ssh 10.40.87.204`, container `docker-php-1`. Fixtures ladder at `/var/tmp/mri134/ladder/src-01000.pdf` ... `src-13000.pdf`.

### Notes for next session
Foreign uncommitted work sits in the workspace from another ticket (`docs/ai-2066/`, plus `.gitignore` and `docs/SOURCES.md` edits) - leave it for that session; don't sweep it into an MRI-134 commit. The earlier PHP benchmark numbers (ladder, filter sweep) were measured through the MedBrief console so they carry the ~19x overhead; that is correct for "what the app delivers today" but the standalone column is the achievable floor.
