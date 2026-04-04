# Contributing to Claude Marketplace

## Adding a Plugin

1. Create a directory under `plugins/` with a kebab-case name (e.g., `plugins/my-tool/`)
2. Add `.claude-plugin/plugin.json` with required fields
3. Add your component files (skills, agents, hooks, `.mcp.json`)
4. Add an entry to `.claude-plugin/marketplace.json` (keep alphabetical order)
5. Submit a pull request

## Plugin Structure

```
plugins/my-tool/
  .claude-plugin/
    plugin.json           # Required: name, description, author
  skills/                 # Optional: skill definitions
    my-skill/
      SKILL.md
  agents/                 # Optional: agent definitions
    my-agent.md
  hooks/                  # Optional: hook configurations
    hooks.json
  .mcp.json               # Optional: MCP server config
```

## plugin.json

```json
{
  "name": "my-tool",
  "description": "Short description of what it does",
  "author": {
    "name": "Your Name"
  }
}
```

## Marketplace Entry

Add to `.claude-plugin/marketplace.json` in the `plugins` array (alphabetical order):

```json
{
  "name": "my-tool",
  "source": "./plugins/my-tool",
  "description": "Short description of what it does",
  "version": "1.0.0",
  "tags": ["relevant", "tags"],
  "category": "development"
}
```

## Guidelines

- Keep descriptions clear and concise
- Test your plugin locally before submitting
- Use semantic versioning
- One plugin per directory
- Keep entries in marketplace.json sorted alphabetically by name
