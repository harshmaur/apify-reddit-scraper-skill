# Examples

Use these examples to translate user requests into Actor input and a good response shape.

## Brand Monitoring

User request:

`Track mentions of Notion on Reddit this month and summarize sentiment.`

Recommended input:

```json
{
  "searchTerms": ["Notion"],
  "searchPosts": true,
  "searchComments": true,
  "searchCommunities": false,
  "searchSort": "new",
  "searchTime": "month",
  "includeNSFW": false,
  "maxPostsCount": 100,
  "maxCommentsCount": 500,
  "maxCommentsPerPost": 25,
  "maxCommunitiesCount": 0,
  "fastMode": true,
  "crawlCommentsPerPost": true,
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Competitor Analysis In One Community

User request:

`Find complaints comparing Linear and Jira in r/startups.`

Recommended input:

```json
{
  "searchTerms": ["Linear Jira"],
  "withinCommunity": "r/startups",
  "searchPosts": false,
  "searchComments": true,
  "searchCommunities": false,
  "searchSort": "relevance",
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
}
```

## Subreddit Trend Research

User request:

`Show me what is trending in r/LocalLLaMA this week.`

Recommended input:

```json
{
  "startUrls": [
    { "url": "https://www.reddit.com/r/LocalLLaMA/" }
  ],
  "searchTerms": [],
  "searchPosts": true,
  "searchComments": false,
  "searchCommunities": false,
  "searchSort": "hot",
  "searchTime": "week",
  "includeNSFW": false,
  "maxPostsCount": 40,
  "maxCommentsCount": 0,
  "maxCommentsPerPost": 0,
  "maxCommunitiesCount": 0,
  "fastMode": true,
  "crawlCommentsPerPost": false,
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Reddit User Research

User request:

`Summarize the posting behavior of this Reddit user.`

Recommended input:

```json
{
  "startUrls": [
    { "url": "https://www.reddit.com/user/example_username/" }
  ],
  "searchTerms": [],
  "searchPosts": true,
  "searchComments": true,
  "searchCommunities": false,
  "searchSort": "new",
  "searchTime": "all",
  "includeNSFW": false,
  "maxPostsCount": 25,
  "maxCommentsCount": 50,
  "maxCommentsPerPost": 0,
  "maxCommunitiesCount": 0,
  "fastMode": true,
  "crawlCommentsPerPost": false,
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Sentiment Dataset Collection

User request:

`Collect a comment dataset about AI coding tools for sentiment analysis.`

Recommended input:

```json
{
  "searchTerms": ["cursor OR codex OR claude code"],
  "searchPosts": true,
  "searchComments": true,
  "searchCommunities": false,
  "searchSort": "top",
  "searchTime": "month",
  "includeNSFW": false,
  "maxPostsCount": 150,
  "maxCommentsCount": 1000,
  "maxCommentsPerPost": 50,
  "maxCommunitiesCount": 0,
  "fastMode": true,
  "crawlCommentsPerPost": true,
  "proxy": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Suggested Response Shape

When presenting results, keep the response structured:

1. Search scope
2. Limits used
3. Item count
4. Three to five notable findings
5. Small sample of representative rows
6. Next recommended parameter change
