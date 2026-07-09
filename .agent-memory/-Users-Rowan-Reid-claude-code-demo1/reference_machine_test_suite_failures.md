---
name: machine-test-suite-failures
description: 6 ~/.claude skill test suites are expected-red on this machine for environmental reasons, not code regressions
metadata:
  type: reference
---

Running `bash ~/.claude/tests/run.sh` on this machine shows **46 suites passing, 6 failing**. All 6 failures are environmental (missing local tooling), NOT code regressions:

- **Missing doc-gen Python venvs** (each needs its skill's `scripts/setup.sh`): `fill-pdf` (pypdf + reportlab), `huble-docx` (python-docx), `huble-pptx` (python-pptx), `medbrief-brand` (python-pptx / python-docx).
- **`claude-cockpit` sibling repo not cloned** at `~/claude_code/claude-cockpit` (`signal_cockpit.py` raises `no usable cockpit`): `ingest-suggestions`, `self-improve`.

Treat these six as known-red until the venvs are built and the cockpit repo is cloned. Confirmed 2026-07-09 during the #sznmbe M4 IDEAS.md per-entry-store catch-up.
