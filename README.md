# Kiro Powers Collection

A curated collection of [Kiro Powers](https://kiro.dev) — ready-to-use integrations that extend your development environment with external tools and services.

## Available Powers

| Power | Description |
|-------|-------------|
| [Atlassian Rovo MCP](./powers/atlassian-rovo-mcp) | Connect to Jira, Confluence, Compass, Bitbucket Cloud, and JSM through the Atlassian Rovo MCP Server |

## How to Use

1. Browse the powers listed above
2. Navigate to the power's folder for detailed documentation
3. Install the power in Kiro to start using it

## Repository Structure

```
powers/
├── atlassian-rovo-mcp/    # Atlassian Cloud integration
│   ├── POWER.md           # Power definition
│   ├── mcp.json           # MCP server configuration
│   └── README.md          # Documentation
└── ...                    # More powers coming soon
```

## Contributing

To add a new power, create a folder under `powers/` with:

- `POWER.md` — The power definition file
- `mcp.json` — MCP server configuration
- `README.md` — Documentation explaining what the power does and how to set it up
