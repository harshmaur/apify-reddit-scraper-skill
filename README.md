# Apify Reddit Scraper — agent skill

A portable [`SKILL.md`](SKILL.md) that teaches Claude Code, Codex, Cursor, Gemini CLI, Windsurf and any other [agentskills.io](https://agentskills.io/specification)-compatible agent how to pull Reddit data with the [Reddit Scraper](https://apify.com/harshmaur/reddit-scraper) Apify Actor: keyword search across Reddit or inside one subreddit, whole-subreddit listings, post permalinks with full comment threads, user histories and community info, with date windows and optional delivery into Slack, Notion, Google Sheets or Airtable through Apify MCP connectors.

The same skill is submitted to [apify/awesome-skills](https://github.com/apify/awesome-skills) as `apify-reddit-scraper`.

## Install

```bash
npx skills add https://github.com/harshmaur/apify-reddit-scraper-skill
```

Or copy this folder to `~/.claude/skills/apify-reddit-scraper` (Claude Code) or `~/.codex/skills/apify-reddit-scraper` (Codex).

## Auth

Either `apify login` (Apify CLI) or `export APIFY_TOKEN=...` from [Apify Console → Integrations](https://console.apify.com/settings/integrations). Agents that prefer MCP can instead connect to `https://mcp.apify.com/?tools=harshmaur/reddit-scraper`.

## What it teaches the agent

- Which input field matches the request: `searchTerms`, `withinCommunity`, `subredditUrls`, `startUrls`, date filters, comment crawling.
- Turning a descriptive topic into literal Reddit keywords (Reddit search is not semantic).
- Cost estimation before running (pay per result, $0.02 per run + $0.002 per item).
- The traps: permalinks in `subredditUrls` silently return nothing, the ~1,000-post ceiling per listing, `/s/` share links, `fastMode` memory.
- Reading the output: `dataType` rows for posts, comments, communities and users.
- Setting up recurring monitoring with Apify Schedules and MCP-connector delivery.

## Contents

- `SKILL.md` — triggers, workflow, routing, troubleshooting
- `references/input-mapping.md` — user intent → input field table with worked examples
- `references/gotchas.md` — cost tables, traps, error recovery, MCP delivery fields
- `agents/openai.yaml`, `assets/` — Codex-facing metadata and icons

## Source Actor

- Store page: https://apify.com/harshmaur/reddit-scraper
- API id: `harshmaur~reddit-scraper`

Disclosure: the skill routes to a paid Actor built by the author. No affiliate links.
