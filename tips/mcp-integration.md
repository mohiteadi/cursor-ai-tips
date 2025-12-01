# Model Context Protocol (MCP) Integration

> MCP is "USB-C for AI" - universal standard for connecting Cursor to databases, APIs, and tools.

---

## What is MCP?

Enables Cursor Agent to:
- Query databases directly
- Manage GitHub PRs/Issues
- Control browsers for testing
- Access custom APIs

---

## Transport Methods

### Stdio (Local)
```
Cursor → spawns process → stdin/stdout JSON-RPC
Best for: Local databases, dev tools
```

### SSE (Remote)
```
Cursor → HTTP → Server-Sent Events
Best for: Team-shared resources, cloud services
```

---

## Configuration: mcp.json

Place in project root or `.cursor/`:

```json
{
  "mcpServers": {
    "server-name": {
      "command": "executable",
      "args": ["arg1", "arg2"],
      "env": { "KEY": "value" }
    }
  }
}
```

---

## Example: PostgreSQL

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${env:DATABASE_URL}"],
      "env": { "DANGEROUSLY_ALLOW_WRITE_OPS": "false" }
    }
  }
}
```

**Usage**: "Check Users table schema and create TypeScript interface"

---

## Example: GitHub

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "GITHUB_PERSONAL_ACCESS_TOKEN", "ghcr.io/github/github-mcp-server"]
    }
  }
}
```

**Usage**: "Find open issues labeled 'bug'" or "Create PR with these changes"

---

## Example: Puppeteer (Browser)

```json
{
  "mcpServers": {
    "browser": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

**Usage**: "Navigate to localhost:3000 and screenshot login page"

---

## Multi-Server Setup

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${env:DATABASE_URL}"]
    },
    "github": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "GITHUB_PERSONAL_ACCESS_TOKEN", "ghcr.io/github/github-mcp-server"]
    },
    "browser": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

---

## Available Servers

| Server | Package | Purpose |
|--------|---------|---------|
| PostgreSQL | `@modelcontextprotocol/server-postgres` | DB queries |
| SQLite | `@modelcontextprotocol/server-sqlite` | Local DB |
| Filesystem | `@modelcontextprotocol/server-filesystem` | File access |
| Puppeteer | `@modelcontextprotocol/server-puppeteer` | Browser |
| GitHub | `ghcr.io/github/github-mcp-server` | PR/Issues |

---

## Security

1. **Never hardcode secrets** - Use `${env:VAR_NAME}`
2. **Read-only default** - `DANGEROUSLY_ALLOW_WRITE_OPS: false`
3. **Limit paths** - Restrict filesystem access
4. **Use official images** - For Docker-based servers

---

## Troubleshooting

- **Not working**: Restart Cursor after adding mcp.json
- **Server error**: Test manually with `npx -y @modelcontextprotocol/server-postgres $DATABASE_URL`
- **Permissions**: Check env vars are set correctly

---

## References

- [Cursor MCP Docs](https://cursor.com/docs/cookbook/building-mcp-server)
- [GitHub MCP Server](https://github.com/github/github-mcp-server)
