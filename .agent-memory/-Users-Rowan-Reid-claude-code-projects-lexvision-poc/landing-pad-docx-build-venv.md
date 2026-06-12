---
name: landing-pad-docx-build-venv
description: "Rebuilding Landing Pad.docx needs the medbrief-brand skill's venv for python-docx; the project venv and base python3 lack it"
metadata: 
  node_type: memory
  type: reference
  originSessionId: bd086078-475a-4d98-8622-e55b4604f9a3
---

UPDATE 2026-06-12: the doc is now hand-edited and was renamed to `docs/kumulus/deliverables/Rowan Kumulus Research.docx`; the spec/`landing-pad-build.py` generator is stale and should NOT be used to rebuild (it would wipe the manual edits, see [[landing-pad-manual-edits]]). The venv below is still the python-docx interpreter to use for editing the docx directly.

Editing or inspecting the Kumulus docx (`Rowan Kumulus Research.docx`, formerly `Landing Pad.docx`) via python-docx needs python-docx, which is NOT installed in the project `.venv` or in base `python3` on this machine. The only working interpreter found is the medbrief-brand skill's venv: `~/.claude/skills/medbrief-brand/scripts/.venv/bin/python3` (python-docx 1.2.0, python3.14).

Rebuild command:

```
~/.claude/skills/medbrief-brand/scripts/.venv/bin/python3 docs/kumulus/deliverables/landing-pad-build.py
```

Verify a rebuild by unzipping the docx and grepping `word/document.xml` for new vs stale strings (the build prints "Wrote ..." but does not validate content). Note: something on this machine has twice silently rebuilt `Landing Pad.docx` to a stale state between sessions; always confirm the docx reflects the current spec after editing. Related: [[content-add-warranted-links]].
