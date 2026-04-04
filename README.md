# Claude Marketplace

A plugin marketplace for Claude Code. Install plugins that add skills, agents, hooks, MCP servers, and LSP servers.

## Install

Add this marketplace to Claude Code:

```
/plugin marketplace add Jylhis/claude-marketplace
```

Then install a plugin:

```
/plugin install example-plugin@jylhis-plugins
```

## Available Plugins

| Plugin | Description |
|--------|-------------|
| `code-explainer` | A skill for explaining code in plain English |
| `example-plugin` | An example plugin demonstrating skills, agents, and hooks |
| `golang-dev` | Go development intelligence: 36 skills + gopls LSP via nix |
| `sqlite-mcp` | MCP server providing read/write access to a local SQLite database |
| `test-generator` | An agent that generates unit tests for source files |
| `todo-guard` | Hook that prevents committing files with TODO/FIXME markers |
| `typescript-lsp` | TypeScript/JavaScript language intelligence via LSP |

## Structure

```
.claude-plugin/
  marketplace.json        # Plugin catalog
plugins/
  code-explainer/         # Skill plugin
  example-plugin/         # Full plugin with skills, agents, hooks
  golang-dev/             # Go skills + gopls LSP
  sqlite-mcp/             # MCP server plugin
  test-generator/         # Agent plugin
  todo-guard/             # Hook plugin
  typescript-lsp/         # LSP server plugin
```

Each plugin contains `.claude-plugin/plugin.json` and its component files (skills, agents, hooks, `.mcp.json`, etc.).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT
