---
date: 2026-04-22
project: /Users/rowanreid/lexvision/claude_code/medbrief
session: Set up three-repo MedBrief workspace with edit target on Azure DevOps
type: wrap-up
tags: [medbrief, workspace-setup, azure-devops, ssh, claudemd]
repos:
  - path: /Users/rowanreid/lexvision/claude_code/medbrief
    commit: 3d9b6ca
  - path: /Users/rowanreid/.claude
    commit: eac8011
domain: medbrief
---

## Session Summary

Set up a three-repo workspace at `lexvision/claude_code/medbrief/` for MedBrief work. Cloned `data_pipelines` (edit target, Azure DevOps, greenfield with only a boilerplate README), `salli-dataset-creation` (context, Bitbucket), and `medbrief` (context, Bitbucket, the main PHP/Symfony + React app). Resolved Azure DevOps SSH: it rejects ed25519 keys, so generated `~/.ssh/id_rsa_azure` (RSA 4096) and added a `Host ssh.dev.azure.com` block in `~/.ssh/config` with `HostkeyAlgorithms +ssh-rsa` and `PubkeyAcceptedAlgorithms +ssh-rsa`. Initialised the workspace as its own git repo with a local identity `rowan.reid@medbrief.co.uk` (Rowan's computer has per-repo identities, no global). Gitignored the sub-repos and wrote a CLAUDE.md describing the ecosystem, the edit-only-in-`data_pipelines` rule, the sibling repos' interfaces (upstream SQL/Jupyter dataset builder; downstream Symfony app with the clinical records DB), and the inferred Python/`.env`/Azure/Bitbucket conventions. Saved a project memory flagging Rowan's MedBrief identity as distinct from his Huble default (he caught me using the Huble email when generating the SSH key).
