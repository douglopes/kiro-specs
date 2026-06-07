---
name: "atlassian-rovo-mcp"
displayName: "Atlassian Rovo MCP"
description: "Access Jira, Confluence, Compass, and Bitbucket Cloud data through the Atlassian Rovo MCP Server. Search, create, and update issues, pages, and components using natural language."
keywords: ["atlassian", "jira", "confluence", "compass", "rovo"]
author: "Atlassian"
---

# Atlassian Rovo MCP

## Overview

The Atlassian Rovo MCP Server is a cloud-hosted gateway that connects your AI development environment to your Atlassian Cloud site. It enables real-time interaction with Jira, Confluence, Compass, Bitbucket Cloud, and Jira Service Management data — all secured by OAuth 2.1 authorization that respects your existing user permissions.

With this power you can search, create, and update Jira issues, Confluence pages, Compass components, and more without leaving your editor. It supports natural language workflows like generating tickets from meeting notes, summarizing documentation, or cross-referencing issues with pages.

## Onboarding

### Prerequisites

- An Atlassian Cloud site with Jira, Confluence, and/or Compass
- Node.js v18+ (only needed if your client requires the `mcp-remote` proxy)
- A modern browser to complete the OAuth 2.1 authorization flow
- Your organization admin must have the Atlassian Rovo MCP Server enabled

### Authentication

The server supports two authentication methods:

1. **OAuth 2.1 (recommended)** — A browser-based consent flow is triggered automatically when you first connect. No manual configuration is required if your MCP client supports OAuth dynamic client registration.

2. **API Token (optional)** — If your organization admin has enabled API token authentication, you can generate a token at:
   https://id.atlassian.com/manage-profile/security/api-tokens

### First-Time Setup

1. When you first use an Atlassian tool, your browser will open for OAuth authorization.
2. Grant consent to the requested Atlassian scopes (Jira, Confluence, Compass as applicable).
3. Once authorized, the connection is active and tools are available immediately.

**Note:** The first user on a site to complete the OAuth consent flow must have access to the Atlassian apps requested by the MCP scopes. After that initial install, other users with access to even a single app (e.g., just Jira) can also connect.

### Server Endpoint

The remote MCP server URL is:

```
https://mcp.atlassian.com/v1/mcp/authv2
```

> **Important:** The older SSE endpoint (`https://mcp.atlassian.com/v1/sse`) is deprecated and will stop working after June 30, 2026.

## Common Workflows

### Jira Workflows

#### Search for Issues
Use natural language or JQL to find issues:
- "Find all open bugs in Project Alpha"
- "Show issues assigned to me in the last 7 days"
- "Search for high-priority stories in sprint 45"

The `searchJiraIssuesUsingJql` tool accepts JQL queries directly.

#### Create and Update Issues
- "Create a story titled 'Redesign onboarding flow' in project ALPHA"
- "Add a comment to ALPHA-123 with the deployment notes"
- "Transition ALPHA-456 to Done"
- "Bulk create five Jira issues from these meeting notes"

#### Get Issue Details
- "Get the details of PROJ-101"
- "What transitions are available for BUG-42?"
- "List all issue types in the MOBILE project"

### Confluence Workflows

#### Search and Read Pages
- "Summarize the Q2 planning page"
- "Search for pages about API design guidelines"
- "List all pages in the Engineering space"

The `searchConfluenceUsingCql` tool accepts CQL queries.

#### Create and Update Pages
- "Create a page titled 'Team Goals Q3' in the Engineering space"
- "Update the architecture decisions page with the new database choice"
- "Add a comment on the release notes page"

#### Navigate Spaces
- "What Confluence spaces do I have access to?"
- "List child pages under the Technical Documentation page"

### Compass Workflows

- "Create a service component based on the current repository"
- "What depends on the api-gateway service?"
- "List components owned by my teams"
- "Import components from this CSV"

### Cross-Product Workflows

- "Link these three Jira tickets to the Release Plan Confluence page"
- "Fetch the Confluence documentation linked to this Compass component"
- "Find all context connected to issue PROJ-100 across Jira, Confluence, and Compass"

The Teamwork Graph tools (`getTeamworkGraphContext`, `getTeamworkGraphObject`) aggregate data across multiple Atlassian products and connected third-party apps.

## Available Tools

### Jira Tools

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_jira | `getJiraIssue`, `getJiraIssueRemoteIssueLinks`, `getJiraIssueTypeMetaWithFields`, `getJiraProjectIssueTypesMetadata`, `getIssueLinkTypes`, `getTransitionsForJiraIssue`, `getVisibleJiraProjects`, `lookupJiraAccountId` | Read issue details, metadata, and project info |
| write_jira | `addCommentToJiraIssue`, `addWorklogToJiraIssue`, `createJiraIssue`, `editJiraIssue`, `transitionJiraIssue` | Create/update issues, add comments and worklogs |
| search_jira | `searchJiraIssuesUsingJql` | Search issues using JQL |

### Confluence Tools

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_confluence | `getConfluencePage`, `getConfluencePageDescendants`, `getConfluencePageFooterComments`, `getConfluencePageInlineComments`, `getConfluenceCommentChildren`, `getConfluenceSpaces`, `getPagesInConfluenceSpace` | Read pages, comments, and spaces |
| write_confluence | `createConfluencePage`, `updateConfluencePage`, `createConfluenceFooterComment`, `createConfluenceInlineComment` | Create/update pages and comments |
| search_confluence | `searchConfluenceUsingCql` | Search content using CQL |

### Compass Tools

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_compass | `getCompassComponent`, `getCompassComponents`, `getCompassComponentActivityEvents`, `getCompassComponentLabels`, `getCompassComponentTypes`, `getCompassCustomFieldDefinitions`, `getCompassComponentsOwnedByMyTeams` | Read component details and metadata |
| write_compass | `createCompassComponent`, `createCompassComponentRelationship`, `createCompassCustomFieldDefinition` | Create components and relationships |

### Jira Service Management Tools (API Token only)

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_jsm | `getJsmOpsAlerts`, `getJsmOpsScheduleInfo`, `getJsmOpsTeamInfo` | Read alerts, schedules, and team info |
| write_jsm | `updateJsmOpsAlert` | Acknowledge, close, or escalate alerts |

### Bitbucket Cloud Tools (API Token only)

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_bitbucket | `bitbucketWorkspace`, `bitbucketRepository`, `bitbucketUser`, `bitbucketDeployment`, `bitbucketPullRequest`, `bitbucketRepoContent`, `bitbucketPipeline`, `bitbucketEnvironment` | Read repos, PRs, pipelines, and deployments |
| write_bitbucket | `bitbucketPullRequest` (create/merge/approve), `bitbucketRepoContent` (branch/commit), `bitbucketPipeline` (run), `bitbucketEnvironment` (manage) | Create PRs, branches, run pipelines |

### Platform Tools

| Permission Group | Tools | Description |
|-----------------|-------|-------------|
| read_teamwork_graph | `getTeamworkGraphContext`, `getTeamworkGraphObject`, `addTeamworkGraphContext` | Cross-product context and relationships |
| search_atlassian | `searchAtlassian`, `fetchAtlassian` | Natural language search via Rovo across Jira and Confluence |
| (shared) | `atlassianUserInfo`, `getAccessibleAtlassianResources` | User details and accessible cloud sites |

## Best Practices

- Use specific JQL/CQL queries rather than broad searches to get precise results
- When creating issues, first use `getJiraProjectIssueTypesMetadata` to understand available issue types and fields
- Use `getTransitionsForJiraIssue` before transitioning an issue to see valid transitions
- For cross-product workflows, leverage the Teamwork Graph tools to discover relationships
- All actions respect your existing Atlassian permissions — you can only access data you have permission to view
- Review high-impact changes (bulk creates, transitions) before confirming

## Troubleshooting

### OAuth Authorization Fails

**Symptoms:** Browser opens but consent flow doesn't complete, or you get redirected with an error.

**Solutions:**
1. Ensure you're signed in to the correct Atlassian account
2. Verify your Atlassian Cloud site has Jira/Confluence/Compass enabled
3. Check with your admin that the Rovo MCP Server is enabled for your organization
4. Try clearing browser cookies for `atlassian.com` and retry

### "Your site admin must authorize this app"

**Cause:** A site admin must complete the OAuth consent flow before other users can connect.

**Solution:** Ask your site admin to connect first, or have them authorize the app from the Connected Apps settings.

### "Your organization admin must authorize access from a domain"

**Cause:** The domain you're connecting from hasn't been allowed.

**Solution:** Ask your organization admin to add the domain in the Atlassian Rovo MCP server settings.

### "You don't have permission to connect from this IP address"

**Cause:** IP allowlisting is enabled and your IP isn't in the allowed list.

**Solution:** Ask your admin to review the IP allowlist configuration and add your network/VPN IP ranges.

### Tools Not Responding or Timing Out

**Solutions:**
1. Check your internet connection
2. Verify the server endpoint URL is `https://mcp.atlassian.com/v1/mcp/authv2`
3. If using `mcp-remote` proxy, ensure your terminal session is still running
4. Re-authenticate by restarting the connection

### Token Expired

**Symptoms:** Previously working tools return authorization errors.

**Solution:** Restart the MCP connection to trigger a fresh OAuth flow. If using `mcp-remote`, re-run the npx command.

## Configuration

**No additional configuration required beyond the MCP server URL.** Authentication is handled automatically via OAuth 2.1 when you first connect.

If your organization requires API token authentication instead of OAuth, generate a token at:
https://id.atlassian.com/manage-profile/security/api-tokens

## Additional Resources

- [Official Getting Started Guide](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/)
- [Supported Tools Reference](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/supported-tools/)
- [IDE Setup Instructions](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/setting-up-ides/)
- [Security & Access Controls](https://support.atlassian.com/security-and-access-policies/docs/understand-atlassian-rovo-mcp-server/)
- [MCP Configuration Reference](https://kiro.dev/docs/mcp/configuration/)

---

**MCP Server:** atlassian-rovo-mcp
**Endpoint:** `https://mcp.atlassian.com/v1/mcp/authv2`
