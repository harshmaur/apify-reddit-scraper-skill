# Apify Reddit Scraper Skill

Portable `SKILL.md` package for Codex and Claude-compatible runtimes that uses the existing Apify Actor API for Reddit scraping.

## What It Does

This skill helps an agent:

- turn Reddit research requests into valid Apify Actor input
- run the existing `harshmaur/reddit-scraper` Actor
- fetch dataset results
- summarize trends, comments, communities, users, and monitoring results

It does not create or require a new MCP server.

## Install

### Codex

Copy this repo into:

```bash
~/.codex/skills/apify-reddit-scraper
```

### Claude

Copy this repo into:

```bash
~/.claude/skills/apify-reddit-scraper
```

## Auth

Set an Apify token before using the skill:

```bash
export APIFY_TOKEN="your-token-here"
```

## Package Contents

- `SKILL.md`: trigger rules and workflow
- `agents/openai.yaml`: Codex-facing metadata
- `references/api-recipes.md`: Apify API examples
- `references/input-mapping.md`: user-intent to Actor-field mapping
- `references/examples.md`: reusable request patterns
- `assets/`: UI icons for skill marketplaces and launchers

## Source Actor

- Apify store: https://apify.com/harshmaur/reddit-scraper
- Actor API ID: `harshmaur~reddit-scraper`

## Suggested Tags

- `skill`
- `skill-md`
- `codex`
- `claude`
- `apify`
- `reddit`
- `agent-skill`

## Publishing Targets

- GitHub
- Smithery Skills
- skillmarketplace.ai
- Agensi
- other SKILL.md-compatible indexes
