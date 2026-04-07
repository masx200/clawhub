# CODEBUDDY.md

This file provides guidance to CodeBuddy Code when working with code in this repository.

## Repository Overview

This is a collection of CodeBuddy Code skills (plugins). Each skill is a self-contained package that extends CodeBuddy Code's capabilities through external API integrations.

## Directory Structure

```
<skill-name>-<version>/
  SKILL.md        # Skill definition with frontmatter (name, description)
  _meta.json      # Metadata: ownerId, slug, version, publishedAt
  scripts/        # Implementation scripts (Python, Bash, or JavaScript)
  references/     # Optional: API documentation or reference files
```

## Skill Packaging Conventions

- Directory names follow `<slug>-<version>` format (e.g., `gitlab-api-0.1.0`)
- SKILL.md must have YAML frontmatter with `name` and `description` fields
- Scripts should be executable and handle errors gracefully
- Environment variables or config files are used for API credentials (never hardcode)

## Current Skills

| Skill | Version | Language | Purpose |
|-------|---------|----------|---------|
| firecrawl-search | 1.0.0 | Python | Web search and scraping via Firecrawl API |
| gitlab-api | 0.1.0 | Bash | GitLab REST API for repository operations |
| gitlab-manager | 1.0.0 | Node.js | GitLab repo/MR/issue management |
| openclaw-tavily-search | 0.1.0 | Python | Web search via Tavily API |

## Environment Variables

Skills require these environment variables:
- `FIRECRAWL_API_KEY` - For firecrawl-search
- `GITLAB_TOKEN` - For gitlab-api and gitlab-manager
- `TAVILY_API_KEY` - For openclaw-tavily-search (also supports `~/.openclaw/.env`)

## Adding a New Skill

1. Create directory: `<skill-slug>-<version>/`
2. Write `SKILL.md` with frontmatter and documentation
3. Add implementation in `scripts/`
4. Create `_meta.json` with ownerId, slug, version, publishedAt

## Script Patterns

- **Python scripts**: Use `argparse` for CLI, `urllib.request` or `requests` for HTTP
- **Bash scripts**: Use `curl` for API calls, `jq` for JSON parsing
- **Node.js scripts**: Use native `fetch`, no external dependencies
