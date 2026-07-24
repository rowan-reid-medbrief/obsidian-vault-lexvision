---
name: ado-primary-code-host
description: "Azure DevOps (MedBrief AI project) is the AI team's primary live code host: 12 git repos, not just work-item tracking. Bitbucket-to-GitHub migration underway (2026)."
metadata: 
  node_type: memory
  type: project
  originSessionId: 87fbc235-0c79-4746-b0b9-c128047bd13c
  modified: 2026-07-24T14:00:44.420Z
---

Azure DevOps (`MedBrief` org → `MedBrief AI` project) is the **primary live
code host for the MedBrief AI team**, not just work-item tracking. It hosts
**12 active git repos** (verified live 2026-06-09 via the azure-devops MCP):
`data_pipelines` (~30 GB), `assisted_chronology` (~22 GB), `expert_match`,
`salli`, `utils`, `chat_with_records`, `hitl`, `doc_preprocessing`,
`em_feedack` (sic), `graph_rule_detection`, `template_repo`, `anonymisation`.

The Bitbucket repos surveyed earlier (`medbrief-ai` archived 2024,
`salli-azure-func`, etc.) are the **older / superseded generation**. The
`medbrief` Symfony monolith genuinely does live in Bitbucket (it's the
downstream app, not AI-team code). Corroborated by the `data_pipelines`
workspace at `~/claude_code/projects/data_pipelines/`, whose edit-target
repo originates from ADO.

The ADO epics map onto the ADO repos (Expert Match→`expert_match`,
SALLi→`salli`, Pseudonymisation→`anonymisation`, Cross utils→`utils`).

**Why:** the original onboarding triage wrongly assumed all code lived in
Bitbucket and ADO was work-items only. This flips a load-bearing assumption
about where current AI-team code lives.

**How to apply:** when looking for current AI-team code, start in ADO, not
Bitbucket. Canonical repo list + lineage note lives at the top of
`notes/00-repo-triage.md`. A full per-repo ADO triage (commit activity,
READMEs, confirmed epic mapping) is still TODO. See [[mcp-servers]] for the
azure-devops MCP config.

**Update (2026-07-24):** Confluence research (governance/AI-tooling investigation)
found MedBrief is actively migrating source control from Bitbucket to GitHub
Enterprise (a "GIT Migration Guide" doc exists with repo-prefix conventions:
web-, micros-, scripts-, msr-, mbwp-), driven partly by the GitHub Copilot
rollout. Scope unconfirmed: the migration guide's prefixes look like the
Bitbucket-hosted apps (the `medbrief` monolith and siblings), not necessarily
the 12 ADO AI-team repos above. Verify current state before assuming either
host is still authoritative. See `notes/18-confluence-ai-data-guidance.md`.
