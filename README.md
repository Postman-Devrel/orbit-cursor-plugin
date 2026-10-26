# Postman Orbit for Cursor

Turn any task into the right API calls.

Describe your task, and Orbit finds public API endpoints that fit, then generates
instructions to call them, from auth to gotchas, so agents can discover, evaluate, and
integrate public APIs.

## What is Orbit?

Orbit is Postman's API discovery service built for AI agents. Instead of a catalog
designed for humans to browse, Orbit returns compact, structured payloads. Each result
carries an `evaluateGuide` that tells the agent what the endpoint is good for and,
just as important, what it can't do, so the agent can decide without trial and error.

## What you get

| Piece | What it does |
|---|---|
| `orbit` MCP server (`mcp.json`) | Connects Cursor to `https://mcp.buildwithorbit.ai/mcp` and exposes the `search` and `integrate` tools. |
| `discover` skill | Drives the workflow: decompose the task, search, read the `evaluateGuide` gaps, then generate an integration brief. |
| `orbit` rule | Agent-requested rule that nudges the agent toward Orbit whenever you need to find or integrate a public API. |

## Install

### From the Cursor Marketplace

Once the plugin is listed, open the Cursor Marketplace, search for **Postman Orbit**
(`orbit`), and install it. The MCP server, skill, and rule are set up for you.

### Local install (development)

Cursor loads plugins placed in `~/.cursor/plugins/local/`:

```bash
git clone https://github.com/Postman-Devrel/orbit-cursor-plugin.git
mkdir -p ~/.cursor/plugins/local
ln -s "$PWD/orbit-cursor-plugin" ~/.cursor/plugins/local/orbit
```

Then run **Developer: Reload Window** from the Command Palette.

### Manual MCP setup (no plugin)

If you only want the tools, add the server to `~/.cursor/mcp.json` (global) or
`.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "orbit": {
      "url": "https://mcp.buildwithorbit.ai/mcp"
    }
  }
}
```

## Authentication

None. Orbit's MCP server is authless: there is no API key, no OAuth flow, and nothing to
configure. Both tools are read-only and open-world (they search a public catalog and
never create or change data).

## Tools

| Tool | Purpose |
|---|---|
| `search` | Find public API endpoints matching a capability query. Returns `id`, `name`, `method`, `url`, `provider`, and an `evaluateGuide` per result. Paginates up to 40 results. |
| `integrate` | Given a task and 1 to 10 endpoints from `search` (2 or 3 works best), returns a task brief: auth, base URLs, ordered request steps, parameters, dependencies, and gotchas. |

## Example prompts

- "Find an API that can send transactional email and one that can geocode addresses."
- "I'm building an app that posts the current weather to Slack. Which APIs should I use?"
- "Use Orbit to find payment APIs that support refunds, and tell me what each one does not support."
- "Generate an integration brief for the PayPal create invoice endpoint."

## How it works

The plugin is a thin workflow layer over Orbit's MCP server. The tool schemas come live
from the server, so Orbit can change its parameters without breaking installed copies of
the plugin. If the MCP server is unreachable, the skill falls back to the documented REST
endpoints in [skills/discover/references/orbit-api.md](skills/discover/references/orbit-api.md).

## Links

- [Orbit](https://www.buildwithorbit.ai)
- [Orbit API reference](https://www.buildwithorbit.ai/api-reference)
- [Orbit MCP server source](https://github.com/postmanlabs/orbit-mcp-server)
- Orbit for other clients: [Claude Code](https://github.com/Postman-Devrel/orbit-claudecode-plugin), [Codex](https://github.com/Postman-Devrel/orbit-codex-plugin)
- Contact: team@buildwithorbit.ai
- [Changelog](CHANGELOG.md) · [Releasing](RELEASING.md) · [Apache-2.0 license](LICENSE)
