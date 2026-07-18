---
name: machine-test-suite-failures
description: "4 test suites are expected-red on this machine (1 shared, 3 environmental), not code regressions"
metadata: 
  node_type: memory
  type: reference
  originSessionId: c73ba0db-4a67-46c8-a490-84b4c7fdfffe
---

As of 2026-07-18, `bash ~/.claude/tests/gate.sh` on this machine expects exactly **4 red suites** (gate PASS means the failed set equals these exactly):

- `registry/test-cross-refs.sh` — the one SHARED code-level red (tracked in `tests/KNOWN-RED.md`: the process-tah-invoice missing-script gap).
- **`claude-cockpit` sibling repo not cloned** at `~/claude_code/claude-cockpit`: `ingest-suggestions`, `self-improve` (machine-local overlay).
- `wiring/test-mcp-config.sh` — no live `mcp.json` on this machine (machine-local overlay, added 2026-07-18 at the gh-copilot s7 merge; clears when #qypmxb registers the MCP servers).

The doc-gen venv failures the 2026-07-09 version of this memory listed (fill-pdf, huble-docx, huble-pptx, medbrief-brand) no longer fail: those venvs were built in the 2026-07-16 catch-up. The machine-local entries live in the gitignored `tests/KNOWN-RED.local.md` overlay.
