# Contributing to Claude Marketplace

## Adding a New Listing

1. Choose the right category: `skills/`, `mcp-servers/`, `hooks/`, or `slash-commands/`
2. Create a directory with a descriptive kebab-case name (e.g., `skills/code-reviewer/`)
3. Add a `manifest.json` following the schema below
4. Add your extension files
5. Add a `README.md` with usage instructions
6. Submit a pull request

## Manifest Schema

```json
{
  "name": "my-extension",
  "version": "1.0.0",
  "description": "Short description of what it does",
  "author": {
    "name": "Your Name",
    "github": "your-github-username"
  },
  "license": "MIT",
  "tags": ["productivity", "code-review"],
  "category": "skills",
  "install": {
    "instructions": "Copy the skill file to ~/.claude/skills/"
  }
}
```

## Guidelines

- Keep descriptions clear and concise
- Include example usage in your README
- Test your extension before submitting
- Use semantic versioning
- One extension per directory
