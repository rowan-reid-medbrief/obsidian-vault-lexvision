---
name: reference_mcp-servers
description: "MCP servers configured globally in Claude Code for this machine, including Teams/M365 access"
metadata: 
  node_type: memory
  type: reference
  originSessionId: cbd050a3-afec-42f3-b726-f44fb38bdae4
---

Three MCP servers are configured globally (`~/.claude.json`, `--scope user`):

| Server | Command | Purpose |
|--------|---------|---------|
| `azure-devops` | `npx -y @azure-devops/mcp@latest MedBrief` | Azure DevOps org "MedBrief" — work items, repos, pipelines |
| `atlassian` | `https://mcp.atlassian.com/v1/mcp` (HTTP) | Jira + Confluence |
| `cli-microsoft365` | `npx -y @pnp/cli-microsoft365-mcp-server@latest` | MS Teams chats, channel messages, meeting transcripts |

## cli-microsoft365 setup notes
- Installed 2026-05-27 via `npm install -g @pnp/cli-microsoft365@latest` and `@pnp/cli-microsoft365-mcp-server@latest`
- Auth: device code flow via `m365 login --appId 04b07795-8ddb-461a-bbee-02f9e1bf7b46` (Microsoft Azure CLI public app ID — used because `m365 setup --appId` is not a valid flag)
- Meeting transcript access is a preview API; cross-user transcripts may need a tenant admin to set an application access policy
