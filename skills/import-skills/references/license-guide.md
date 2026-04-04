# License Compatibility Guide

## License Categories

### Permissive (Auto-approved)

These licenses allow redistribution, modification, and inclusion in this marketplace without restrictions beyond attribution:

| License | SPDX ID | Notes |
|---------|---------|-------|
| MIT | MIT | Most common for skills repos |
| Apache 2.0 | Apache-2.0 | Requires NOTICE file if present |
| BSD 2-Clause | BSD-2-Clause | "Simplified" BSD |
| BSD 3-Clause | BSD-3-Clause | "New" BSD, no endorsement clause |
| ISC | ISC | Functionally equivalent to MIT |
| Unlicense | Unlicense | Public domain dedication |
| CC0 1.0 | CC0-1.0 | Public domain dedication |
| MPL 2.0 | MPL-2.0 | File-level copyleft, compatible |
| 0BSD | 0BSD | Zero-clause BSD |
| Zlib | Zlib | Permissive, rare |

### Copyleft (Requires Confirmation)

These licenses have share-alike requirements that may affect the marketplace:

| License | SPDX ID | Risk |
|---------|---------|------|
| GPL 2.0 | GPL-2.0-only | Derived works must also be GPL |
| GPL 3.0 | GPL-3.0-only | Derived works must also be GPL |
| AGPL 3.0 | AGPL-3.0-only | Network use triggers copyleft |
| LGPL 2.1 | LGPL-2.1-only | Library exception, may be OK |
| LGPL 3.0 | LGPL-3.0-only | Library exception, may be OK |

When encountering copyleft licenses:
1. Warn the user about the implications
2. Explain that importing may require the marketplace or plugin to adopt the same license
3. Ask for explicit confirmation before proceeding
4. If confirmed, note the license prominently in the plugin README

### No License

If no license is detected:
- The code is under exclusive copyright by default
- Redistribution is NOT permitted without explicit permission from the author
- Do NOT import — inform the user and suggest they contact the repo owner

## Checking Licenses

### Repository-Level License

```bash
# GitHub API returns detected license
gh api "repos/{owner}/{repo}" -q '.license.spdx_id'

# Fetch full LICENSE file
gh api "repos/{owner}/{repo}/contents/LICENSE" -q '.content' | base64 -d
```

### Per-Skill License

Some repos include license fields in skill frontmatter:

```yaml
---
name: my-skill
license: MIT
metadata:
  author: someone
---
```

Per-skill licenses override the repository license for that specific skill. Check for `license:` in YAML frontmatter when fetching each skill.

### Multi-License Repos

Some repositories contain skills from multiple authors with different licenses. In such cases:
- Check each skill's frontmatter for a `license` field
- If per-skill licenses differ, group skills by license in the README Sources section
- Ensure all licenses are in the auto-approved or confirmed category

## Attribution Requirements

### MIT / BSD / ISC
- Include original copyright notice
- Reference the source repo and author in README

### Apache 2.0
- Include original copyright notice
- Reference the source repo and author in README
- If the source repo has a NOTICE file, include its contents or reference it

### MPL 2.0
- Keep original license headers in modified files
- Reference the source repo in README

## README Sources Format

```markdown
## Sources

Skills are sourced from:

- [owner/repo](https://github.com/owner/repo) — N skills by Author Name (MIT)
- [other/repo](https://github.com/other/repo) — M skills by Other Author (Apache-2.0)

## License

Skills retain the licenses of their original sources. See the repositories above.
```
