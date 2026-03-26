---
name: apify-reddit-scraper
description: Use this skill when the user needs Reddit posts, comments, users, communities, trend research, brand monitoring, competitor analysis, or sentiment datasets from Reddit via the Apify Actor API instead of building a new scraper or MCP server.
---

# Apify Reddit Scraper

Use this skill to run the existing Apify Actor `harshmaur/reddit-scraper` and turn Reddit requests into valid Actor input, dataset fetches, and concise analysis.

## When To Use

Use this skill when the user wants any of the following:

- scrape one or more Reddit URLs
- search Reddit posts, comments, or communities by keyword
- limit a search to a single subreddit
- collect subreddit trend data
- extract comments for sentiment or qualitative analysis
- inspect a Reddit user profile, posts, or comments
- monitor mentions of a brand, product, or competitor on Reddit

Do not use this skill when:

- the user only wants a quick manual browsing answer
- the task requires a new MCP server
- the task is unrelated to Reddit data collection

## Required Setup

Before calling the Apify API, confirm one of these auth paths:

- `APIFY_TOKEN` is available in the environment
- the user explicitly provides an Apify token for this task

Default Actor identifier:

- API path form: `harshmaur~reddit-scraper`
- store page form: `harshmaur/reddit-scraper`

Default proxy block for reliable scraping:

```json
{
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Workflow

### 1. Pick the lowest-friction input mode

Choose the input shape that matches the user request:

- direct Reddit URLs: use `startUrls`
- keyword search: use `searchTerms`
- search inside one subreddit: use `searchTerms` plus `withinCommunity`
- user profile or subreddit page: use `startUrls`

If the user asks for subreddit-scoped search, `withinCommunity` must use the format `r/name`.

### 2. Build Actor input with safe defaults

Unless the user asks otherwise, use these defaults:

```json
{
  "searchPosts": true,
  "searchComments": false,
  "searchCommunities": false,
  "crawlCommentsPerPost": false,
  "searchSort": "new",
  "searchTime": "all",
  "includeNSFW": false,
  "maxPostsCount": 25,
  "maxCommentsCount": 50,
  "maxCommentsPerPost": 10,
  "maxCommunitiesCount": 10,
  "fastMode": true,
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

Use `fastMode: false` when accurate subreddit comment search matters. The underlying actor docs warn that fast mode is less accurate for comment searches within subreddits.

### 3. Choose sync or async execution

Use the synchronous endpoint when the scrape is small enough to finish inside the API timeout. Use the async flow for larger jobs, broad searches, large subreddit pulls, or heavy comment collection.

- Small jobs: `run-sync-get-dataset-items`
- Larger jobs: start a run, wait for completion, then fetch dataset items

See [references/api-recipes.md](./references/api-recipes.md) for exact examples.

### 4. Summarize results for the user

Return:

- what was searched
- the exact Actor input you used
- item count
- notable findings or themes
- a compact sample of the output
- the dataset or run URL if available
- any follow-up options, such as exporting more rows or switching sort/time range

## Input Mapping

Map user phrasing to Actor fields instead of inventing new API parameters.

- “scrape these Reddit links” -> `startUrls`
- “find mentions of X” -> `searchTerms`
- “only in r/startups” -> `withinCommunity: "r/startups"`
- “comments only” -> `searchComments: true`, `searchPosts: false`
- “also pull comments under each post” -> `crawlCommentsPerPost: true`
- “user profile” or “subreddit page” -> URL in `startUrls`

See [references/input-mapping.md](./references/input-mapping.md) for the full mapping table.

## Output Guidelines

Prefer concise, decision-ready outputs:

1. State the search scope and limits.
2. Call out the strongest trends, entities, complaints, or opportunities.
3. Quote or sample only a few representative rows.
4. Mention if the run was truncated by limits.
5. Suggest the next best parameter change if the result set is too broad or too small.

## Troubleshooting

- Missing token: ask for `APIFY_TOKEN` or tell the user how to set it.
- No results: widen `searchTime`, relax subreddit scoping, or increase limits.
- Invalid subreddit scope: require `withinCommunity` in the form `r/subreddit`.
- Slow or timeout-prone run: switch from sync to async.
- Comment-search accuracy issue: retry with `fastMode: false`.
- Scraping reliability issue: keep Apify residential proxy enabled.

## References

- API recipes and `curl` flows: [references/api-recipes.md](./references/api-recipes.md)
- Intent-to-input mapping: [references/input-mapping.md](./references/input-mapping.md)
- Reusable user-facing examples: [references/examples.md](./references/examples.md)
