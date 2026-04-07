# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a collection of user-invocable skills for Claude Code. Each skill is a self-contained extension that can be invoked via slash commands (e.g., `/firecrawl-search`, `/gitlab-api`).

## Skill Structure

Each skill follows a consistent directory structure:

```
skill-name-version/
├── SKILL.md              # Skill documentation with frontmatter
├── _meta.json            # Skill metadata (owner, slug, version, publish date)
├── references/           # Optional API documentation
└── scripts/              # Implementation scripts
    └── executable_files
```

### Required Files

- **SKILL.md**: Must contain frontmatter with `name` and `description` fields:
  ```yaml
  ---
  name: skill-name
  description: Brief description of when to use this skill
  ---
  ```

- **_meta.json**: Contains skill metadata:
  ```json
  {
    "ownerId": "...",
    "slug": "skill-name",
    "version": "x.x.x",
    "publishedAt": timestamp
  }
  ```

### Scripts

Scripts can be written in any language but should be:
- Executable (proper shebang)
- Self-contained (no external project dependencies)
- Environment variable driven for configuration

Common script patterns:
- Python: `#!/usr/bin/env python3` with `argparse` for CLI
- Bash: `#!/bin/bash` with subcommands pattern
- Node.js: `#!/usr/bin/env node` using built-in `fetch` (Node 18+)

## Testing Skills

Test skills by running their scripts directly:

```bash
# Python scripts
python3 skill-name-version/scripts/script.py --arg value

# Bash scripts
bash skill-name-version/scripts/script.sh command arg1 arg2

# Node.js scripts
node skill-name-version/scripts/script.js command arg1 arg2
```

### Environment Variables

Each skill documents its required environment variables in its SKILL.md. Common patterns:
- API keys in `.env` files or environment variables
- Config files in `~/.config/` or `~/.openclaw/`

## Adding or Modifying Skills

When creating a new skill:

1. Create directory following `name-version` pattern
2. Create `SKILL.md` with frontmatter and usage documentation
3. Create `_meta.json` with metadata
4. Add executable scripts in `scripts/` directory
5. Document any required environment variables
6. Test scripts directly before publishing

When modifying an existing skill:
- Update version in `_meta.json` for published skills
- Update `SKILL.md` if API or usage changes
- Maintain backward compatibility when possible
- Test modified functionality before committing

## Current Skills

- **firecrawl-search** ([firecrawl-search-1.0.0/](firecrawl-search-1.0.0/)): Web search and scraping via Firecrawl API. Python scripts for search, scrape, and crawl operations.
- **gitlab-api** ([gitlab-api-0.1.0/](gitlab-api-0.1.0/)): GitLab repository operations via REST API. Bash script for file operations.
- **gitlab-manager** ([gitlab-manager-1.0.0/](gitlab-manager-1.0.0/)): GitLab repository, MR, and issue management. Node.js script.
- **openclaw-tavily-search** ([openclaw-tavily-search-0.1.0/](openclaw-tavily-search-0.1.0/)): Web search via Tavily API. Python script with multiple output formats.
