# Claude Marketplace

A marketplace for discovering, sharing, and installing Claude Code extensions — skills, MCP servers, slash commands, and hooks.

## Structure

```
marketplace/
  skills/          # Reusable Claude Code skills (.md)
  mcp-servers/     # MCP server configurations
  hooks/           # Pre/post hooks for Claude Code
  slash-commands/  # Custom slash commands
```

## How It Works

Each listing is a directory containing:

- `manifest.json` — metadata (name, version, description, author, tags)
- The extension files themselves
- `README.md` — usage instructions

## Contributing

1. Fork this repository
2. Create a new directory under the appropriate category
3. Add a `manifest.json` and your extension files
4. Submit a pull request

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

MIT
