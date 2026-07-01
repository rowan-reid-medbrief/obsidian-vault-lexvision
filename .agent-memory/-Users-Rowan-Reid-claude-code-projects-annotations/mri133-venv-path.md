---
name: mri133-venv-path
description: "In the annotations project the Python venv is at poc/.venv; Bash cwd resets to repo root each call, so use absolute venv paths."
metadata: 
  node_type: memory
  type: project
  originSessionId: 285f01fd-a836-44ba-afe3-a138d5010f9b
---

Running Python in this project: the virtualenv lives at `poc/.venv/bin/python` (under `poc/`, not the repo root), because the CLI package and its `pyproject.toml` sit in `poc/`. The `./mri133` launcher and `./setup.sh` handle this for the CLI, but ad-hoc `python3 -c ...` invocations do not.

Each Bash tool call starts from the project root regardless of earlier `cd`s, so a bare `.venv/bin/python3` (or a relative path assuming a previous `cd poc`) fails with "no such file or directory". Use the absolute path `/Users/Rowan.Reid/claude_code/projects/annotations/poc/.venv/bin/python3`, or `cd` within the same compound command. Tests run with `cd poc && .venv/bin/python -m pytest`. See [[mri-133-project]].
