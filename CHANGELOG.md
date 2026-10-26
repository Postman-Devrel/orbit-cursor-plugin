# Changelog

All notable changes to this plugin are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Add your changes under `[Unreleased]` in every PR. The release workflow moves that
section into a dated, versioned entry when a release is cut. See [RELEASING.md](RELEASING.md).

## [Unreleased]

## [1.0.0] - 2026-10-26

### Added

- Initial release of the Orbit plugin for Cursor.
- Bundled Orbit MCP server (`mcp.json`): `https://mcp.buildwithorbit.ai/mcp`, remote
  Streamable HTTP, no authentication. Exposes the read-only `search` and `integrate` tools.
- `discover` skill: decompose a task into capability queries, search Orbit, read each
  endpoint's `evaluateGuide`, and generate an integration task brief for the endpoints
  you pick. Includes a REST fallback reference (`skills/discover/references/orbit-api.md`).
- `orbit` agent-requested rule that points the agent at Orbit when you need to find or
  integrate a public API.

[Unreleased]: https://github.com/Postman-Devrel/orbit-cursor-plugin/compare/1.0.0...HEAD
[1.0.0]: https://github.com/Postman-Devrel/orbit-cursor-plugin/releases/tag/1.0.0
