# Kiro Powers — Atlassian Rovo MCP

This repository contains a [Kiro Power](https://kiro.dev) that integrates your development environment with Atlassian Cloud products through the Atlassian Rovo MCP Server.

## What This Power Does

The **Atlassian Rovo MCP** power connects Kiro directly to your Atlassian Cloud site, enabling you to interact with multiple Atlassian products without leaving your editor:

| Product | Capabilities |
|---------|-------------|
| **Jira** | Search issues (JQL), create/update issues, transition statuses, add comments and worklogs |
| **Confluence** | Search/read/create/update pages, browse spaces, manage comments |
| **Compass** | View and create service components, explore dependencies |
| **Bitbucket Cloud** | Read repos and PRs, create branches, run pipelines (API token only) |
| **Jira Service Management** | Read alerts and schedules, acknowledge/close alerts (API token only) |
| **Cross-product** | Teamwork Graph for discovering relationships across all products |

## Authentication & Permissions

### OAuth 2.1 (Recommended)

The power uses **OAuth 2.1 with dynamic client registration**. When you first use any Atlassian tool:

1. Your browser opens automatically with the Atlassian consent screen
2. You grant access to the requested scopes (Jira, Confluence, Compass, etc.)
3. Once authorized, the connection is active immediately — no manual token configuration needed

> **First user on a site:** Must have access to all Atlassian apps requested by the MCP scopes. After that initial install, other users can connect with access to even a single app.

### API Token (Alternative)

If your organization prefers API token authentication:

1. Generate a token at: https://id.atlassian.com/manage-profile/security/api-tokens
2. Configure it in your MCP settings

### Permission Model

All actions respect your existing Atlassian Cloud permissions:

- You can only access data you already have permission to view
- Write operations require the same permissions as using the Atlassian UI
- Tools are grouped by permission scopes (`read_jira`, `write_jira`, `search_jira`, etc.)
- Organization admins control whether the Rovo MCP Server is enabled for users

### Access Controls

Your organization admin can enforce:

- **Domain allowlisting** — restrict which domains can connect
- **IP allowlisting** — restrict connections to specific IP ranges/VPNs
- **App authorization** — require admin approval before users can connect

## Getting Started

### Prerequisites

- An Atlassian Cloud site with Jira, Confluence, and/or Compass
- Node.js v18+ (if your client requires the `mcp-remote` proxy)
- Organization admin must have Rovo MCP Server enabled

### Installation

1. Install this power in Kiro
2. The MCP server endpoint is pre-configured: `https://mcp.atlassian.com/v1/mcp/authv2`
3. Use any Atlassian tool — the OAuth flow triggers automatically on first use

## Example Usage

```
"Find all open bugs assigned to me in Project ALPHA"
"Create a story titled 'Implement dark mode' in project MOBILE"
"Summarize the Q3 planning page in Confluence"
"What depends on the api-gateway component in Compass?"
```

## Resources

- [Official Getting Started Guide](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/)
- [Supported Tools Reference](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/supported-tools/)
- [IDE Setup Instructions](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/setting-up-ides/)
- [Security & Access Controls](https://support.atlassian.com/security-and-access-policies/docs/understand-atlassian-rovo-mcp-server/)
