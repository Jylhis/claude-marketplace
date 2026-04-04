---
name: import-skills
description: "This skill should be used when the user asks to \"import skills\", \"add skills from repo\", \"import from GitHub\", \"pull skills from\", \"fetch skills from\", \"copy skills from\", \"add external skills\", \"merge skills into plugin\", or provides a GitHub repository URL containing Claude Code skills to import into this marketplace. Handles license validation, plugin creation/merging, source attribution, and quality review."
argument-hint: "<github-repo-url> [--plugin <existing-plugin-name>] [--new-plugin <name>]"
user-invocable: true
allowed-tools: ["Read", "Write", "Edit", "Bash", "Glob", "Grep", "Agent", "WebFetch", "AskUserQuestion"]
---

# Import Skills from External Repositories

Import Claude Code skills from external GitHub repositories into this marketplace. Handle license validation, plugin creation or merging, README source attribution, and quality review.

## Workflow

### Prerequisites

Before starting, verify GitHub CLI authentication:
```bash
gh auth status
```
If not authenticated, inform the user and ask them to run `! gh auth login`.

### Step 1: Analyze Source Repository

Fetch the repository structure to identify available skills. If API calls return 404 or 403, verify the repo URL is correct and accessible.

```bash
# List repo contents
gh api "repos/{owner}/{repo}/git/trees/HEAD?recursive=1" --jq '.tree[] | .path'

# Check for metadata
gh api "repos/{owner}/{repo}/contents/metadata.json" -q '.content' | base64 -d

# Check for license
gh api "repos/{owner}/{repo}/license" -q '.license.spdx_id'
gh api "repos/{owner}/{repo}/contents/LICENSE" -q '.content' | base64 -d | head -5
```

Identify skills by looking for `skills/*/SKILL.md` paths in the tree. Also check for `commands/`, `agents/`, and other plugin components that may need to come along.

### Step 2: Validate Licenses

Before importing, verify the source repository has an acceptable open-source license.

**Allowed licenses** (compatible with redistribution):
- MIT
- Apache-2.0
- BSD-2-Clause, BSD-3-Clause
- ISC
- MPL-2.0
- Unlicense, CC0-1.0

**Blocked licenses** (require user confirmation):
- GPL-2.0, GPL-3.0, AGPL-3.0 — copyleft may affect the marketplace
- LGPL-2.1, LGPL-3.0 — requires careful handling
- No license found — warn user, cannot redistribute without permission

Check using the GitHub API:
```bash
gh api "repos/{owner}/{repo}" -q '.license.spdx_id'
```

If the license is blocked or missing, inform the user and ask whether to proceed. Do not import without explicit confirmation.

Also check individual skill files for per-skill license fields in frontmatter (e.g., `license: MIT`).

For the full compatibility matrix and attribution requirements, see `references/license-guide.md`.

### Step 3: Select Skills to Import

Present the full list of discovered skills to the user with a summary table:

```
| # | Skill Name | Description (short) |
|---|------------|---------------------|
| 1 | skill-a    | Does X              |
| 2 | skill-b    | Does Y              |
```

Ask the user which skills to import, or whether to import all. Also identify skills that should be **excluded** — typically framework-specific meta skills (e.g., routers, skill creators, dynamic loaders) that depend on the source project's infrastructure.

### Step 4: Determine Target Plugin

Decide whether to create a new plugin or merge into an existing one.

**Check existing plugins:**
```bash
ls plugins/
```

**Merge criteria** — merge into an existing plugin when:
- The skills share the same language/domain (e.g., Rust skills into `rust-dev`)
- The existing plugin was designed to aggregate skills from multiple sources
- The user explicitly requests merging with `--plugin <name>`

**Create new plugin when:**
- No matching plugin exists
- The skills represent a distinct domain
- The user explicitly requests with `--new-plugin <name>`

If unclear, ask the user:
> "These skills could fit into the existing `{plugin}` plugin or become a new plugin. Which do you prefer?"

When creating a new plugin, use the `plugin-dev:create-plugin` skill by invoking the Skill tool:
```
Skill(skill: "plugin-dev:create-plugin", args: "<plugin-name>")
```

### Step 5: Fetch and Write Skills

For each selected skill, fetch the SKILL.md and any supporting files.

```bash
# Fetch SKILL.md
gh api "repos/{owner}/{repo}/contents/skills/{skill-name}/SKILL.md" -q '.content' | base64 -d

# Check for supporting directories
gh api "repos/{owner}/{repo}/contents/skills/{skill-name}" -q '.[].name'

# Fetch references, examples, scripts, assets if they exist
gh api "repos/{owner}/{repo}/contents/skills/{skill-name}/references" -q '.[].name'
```

Write each skill to `plugins/{plugin-name}/skills/{skill-name}/SKILL.md`. Preserve the original content exactly — do not modify skill bodies.

For supporting files (references/, examples/, scripts/, assets/), fetch and write them too.

Use parallel Agent calls to fetch multiple skills simultaneously for speed.

### Step 6: Update Plugin README

After importing, update (or create) the plugin README with:

1. **Install instructions** — `/plugin install {plugin-name}@jylhis-plugins`
2. **Skills table** — all skills with name and short description
3. **Sources section** — credit the original repository with URL, author, and license

Example Sources section:
```markdown
## Sources

Skills are sourced from:

- [{owner}/{repo}](https://github.com/{owner}/{repo}) — {count} skills by {author} ({license})

## License

Skills retain the licenses of their original sources. See the repositories above.
```

When merging into a plugin that already has sources, **append** to the existing Sources list rather than replacing it.

### Step 7: Update Marketplace Manifest

If a new plugin was created, add it to `.claude-plugin/marketplace.json`:

```json
{
  "name": "{plugin-name}",
  "source": "./plugins/{plugin-name}",
  "description": "{description}",
  "version": "1.0.0",
  "tags": [...],
  "category": "development"
}
```

Read the current marketplace.json first and append the new entry to the `plugins` array.

### Step 8: Quality Review

After importing, run the skill-reviewer agent on a sample of imported skills (at least 3, or all if fewer than 5):

```
Agent(subagent_type: "plugin-dev:skill-reviewer", prompt: "Review the skill at plugins/{plugin}/skills/{skill}/SKILL.md")
```

Also run the plugin-validator agent:

```
Agent(subagent_type: "plugin-dev:plugin-validator", prompt: "Validate the plugin at plugins/{plugin}/")
```

Report any issues found and offer to fix them.

## Key Rules

- **Never import without license validation** — check before fetching any skill content
- **Preserve original skill content** — do not rewrite or restyle imported skills
- **Always attribute sources** — every import must be credited in the README
- **Ask before merging** — when target plugin is ambiguous, ask the user
- **Validate after import** — always run skill-reviewer and plugin-validator

## Additional Resources

### Reference Files

- **`references/license-guide.md`** — Detailed license compatibility rules and edge cases
