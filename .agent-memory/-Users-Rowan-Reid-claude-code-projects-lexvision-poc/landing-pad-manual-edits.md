---
name: landing-pad-manual-edits
description: "Rowan hand-edits the Landing Pad doc directly (now renamed Rowan Kumulus Research.docx); check the live docx before any edit, do not rebuild from spec"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: d641061c-f1de-4c68-87c8-b171e97a6f6e
---

From 2026-06-12, Rowan is making manual edits directly in the Kumulus working doc. On 2026-06-12 he renamed it from `Landing Pad.docx` to `docs/kumulus/deliverables/Rowan Kumulus Research.docx` (edit that file now, not the old name). Before making ANY change, first inspect the current docx to detect what he has changed. Inspect via python-docx, and when checking whether links survive an edit, read the `w:hyperlink` relationships, not just `cell.text` (which never shows URLs).

**Why:** The docx was a generated artefact (`landing-pad.spec.json` → `landing-pad-build.py` → `.docx`). Once Rowan edits the docx by hand, the spec is stale and a rebuild-from-spec would silently overwrite his manual edits.

**How to apply:** Never run `landing-pad-build.py` to regenerate the whole docx without first reconciling. To make a change, either (a) read the live docx, identify Rowan's edits, and edit the docx in place, or (b) if the spec must be used, first fold his manual edits back into `landing-pad.spec.json` so nothing is lost. When in doubt, surface the detected manual edits to Rowan before proceeding. See [[landing-pad-docx-build-venv]].
