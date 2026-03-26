# API Recipes

Use these recipes when the skill needs concrete Apify API calls.

## Prerequisites

- Actor API ID: `harshmaur~reddit-scraper`
- Environment token:

```bash
export APIFY_TOKEN="your-token-here"
```

## 1. Small synchronous keyword search

Use for small searches that should finish quickly.

```bash
curl -sS \
  -X POST \
  "https://api.apify.com/v2/acts/harshmaur~reddit-scraper/run-sync-get-dataset-items?token=${APIFY_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "searchTerms": ["openai codex"],
    "searchPosts": true,
    "searchComments": false,
    "searchCommunities": false,
    "searchSort": "new",
    "searchTime": "month",
    "includeNSFW": false,
    "maxPostsCount": 25,
    "maxCommentsCount": 0,
    "maxCommentsPerPost": 0,
    "maxCommunitiesCount": 0,
    "fastMode": true,
    "crawlCommentsPerPost": false,
    "proxy": {
      "useApifyProxy": true,
      "apifyProxyGroups": ["RESIDENTIAL"]
    }
  }'
```

## 2. Small synchronous subreddit URL scrape

Use for direct subreddit, post, or user URLs.

```bash
curl -sS \
  -X POST \
  "https://api.apify.com/v2/acts/harshmaur~reddit-scraper/run-sync-get-dataset-items?token=${APIFY_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "startUrls": [
      { "url": "https://www.reddit.com/r/technology/" }
    ],
    "searchTerms": [],
    "searchPosts": true,
    "searchComments": false,
    "searchCommunities": false,
    "searchSort": "hot",
    "searchTime": "all",
    "includeNSFW": false,
    "maxPostsCount": 20,
    "maxCommentsCount": 20,
    "maxCommentsPerPost": 10,
    "maxCommunitiesCount": 0,
    "fastMode": true,
    "crawlCommentsPerPost": false,
    "proxy": {
      "useApifyProxy": true,
      "apifyProxyGroups": ["RESIDENTIAL"]
    }
  }'
```

## 3. Accurate comment search inside one subreddit

Turn off fast mode when comment precision matters.

```bash
curl -sS \
  -X POST \
  "https://api.apify.com/v2/acts/harshmaur~reddit-scraper/run-sync-get-dataset-items?token=${APIFY_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "searchTerms": ["pricing complaints"],
    "withinCommunity": "r/SaaS",
    "searchPosts": false,
    "searchComments": true,
    "searchCommunities": false,
    "searchSort": "new",
    "searchTime": "year",
    "includeNSFW": false,
    "maxPostsCount": 0,
    "maxCommentsCount": 200,
    "maxCommentsPerPost": 0,
    "maxCommunitiesCount": 0,
    "fastMode": false,
    "crawlCommentsPerPost": false,
    "proxy": {
      "useApifyProxy": true,
      "apifyProxyGroups": ["RESIDENTIAL"]
    }
  }'
```

## 4. Start an async run

Use when the scrape may exceed the synchronous timeout.

```bash
curl -sS \
  -X POST \
  "https://api.apify.com/v2/acts/harshmaur~reddit-scraper/runs?token=${APIFY_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "searchTerms": ["cursor ai"],
    "searchPosts": true,
    "searchComments": true,
    "searchCommunities": false,
    "searchSort": "top",
    "searchTime": "month",
    "includeNSFW": false,
    "maxPostsCount": 200,
    "maxCommentsCount": 1000,
    "maxCommentsPerPost": 50,
    "maxCommunitiesCount": 0,
    "fastMode": true,
    "crawlCommentsPerPost": true,
    "proxy": {
      "useApifyProxy": true,
      "apifyProxyGroups": ["RESIDENTIAL"]
    }
  }'
```

The response includes a run ID and usually a default dataset ID.

## 5. Poll async run status

```bash
curl -sS \
  "https://api.apify.com/v2/actor-runs/<RUN_ID>?token=${APIFY_TOKEN}"
```

Wait until the status is `SUCCEEDED` before fetching results.

## 6. Fetch dataset items from an async run

```bash
curl -sS \
  "https://api.apify.com/v2/datasets/<DATASET_ID>/items?token=${APIFY_TOKEN}&format=json&clean=true"
```

## 7. Export CSV

```bash
curl -sS \
  "https://api.apify.com/v2/datasets/<DATASET_ID>/items?token=${APIFY_TOKEN}&format=csv&clean=true" \
  -o reddit-results.csv
```

## Notes

- At least one of `startUrls` or `searchTerms` must be present.
- `withinCommunity` must look like `r/programming`.
- Large jobs should prefer async execution.
- Keep the proxy block unless the user has a clear reason not to.
