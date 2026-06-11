---
name: landing-pad-docx-build-venv
description: "Rebuilding Landing Pad.docx needs the medbrief-brand skill's venv for python-docx; the project venv and base python3 lack it"
metadata: 
  node_type: memory
  type: reference
  originSessionId: bd086078-475a-4d98-8622-e55b4604f9a3
---

Rebuilding `docs/kumulus/deliverables/Landing Pad.docx` from `landing-pad.spec.json` via `landing-pad-build.py` needs python-docx, which is NOT installed in the project `.venv` or in base `python3` on this machine. The only working interpreter found is the medbrief-brand skill's venv: `~/.claude/skills/medbrief-brand/scripts/.venv/bin/python3` (python-docx 1.2.0, python3.14).

Rebuild command:

```
~/.claude/skills/medbrief-brand/scripts/.venv/bin/python3 docs/kumulus/deliverables/landing-pad-build.py
```

Verify a rebuild by unzipping the docx and grepping `word/document.xml` for new vs stale strings (the build prints "Wrote ..." but does not validate content). Note: something on this machine has twice silently rebuilt `Landing Pad.docx` to a stale state between sessions; always confirm the docx reflects the current spec after editing. Related: [[content-add-warranted-links]].
