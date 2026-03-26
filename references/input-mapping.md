# Input Mapping

Map user intent to the Actor's real input fields.

## Core Rules

- Use `startUrls` for direct Reddit URLs.
- Use `searchTerms` for keyword-driven searches.
- Use `withinCommunity` only with a single subreddit in the form `r/name`.
- Use `searchPosts`, `searchComments`, and `searchCommunities` to select result type.
- Use `crawlCommentsPerPost` when the user wants comments under matching posts.

## Intent Mapping Table

| User intent | Actor fields |
| --- | --- |
| Scrape a subreddit page | `startUrls: [{ "url": "https://www.reddit.com/r/<name>/" }]` |
| Scrape a specific Reddit post | `startUrls` with the post URL |
| Scrape a Reddit user | `startUrls` with the user URL |
| Search Reddit for a keyword | `searchTerms`, `searchPosts: true` |
| Search comments for a keyword | `searchTerms`, `searchComments: true`, `searchPosts: false` |
| Search communities by keyword | `searchTerms`, `searchCommunities: true`, `searchPosts: false`, `searchComments: false` |
| Limit keyword search to one subreddit | `withinCommunity: "r/<name>"` |
| Pull comments from found posts | `crawlCommentsPerPost: true` plus non-zero comment limits |
| Prioritize fresh posts | `searchSort: "new"` |
| Prioritize popular posts | `searchSort: "top"` or `searchSort: "hot"` |
| Limit to recent period | `searchTime: "hour" | "day" | "week" | "month" | "year"` |
| Include adult content | `includeNSFW: true` |
| Improve comment-search accuracy in a subreddit | `fastMode: false` |

## Recommended Defaults

Use these unless the user asks for something else:

```json
{
  "searchPosts": true,
  "searchComments": false,
  "searchCommunities": false,
  "searchSort": "new",
  "searchTime": "all",
  "includeNSFW": false,
  "maxPostsCount": 25,
  "maxCommentsCount": 50,
  "maxCommentsPerPost": 10,
  "maxCommunitiesCount": 10,
  "fastMode": true,
  "crawlCommentsPerPost": false
}
```

## Limits Guidance

- `maxPostsCount`: cap top-level posts returned
- `maxCommentsCount`: cap comment results or collected comments
- `maxCommentsPerPost`: cap comments gathered per post when `crawlCommentsPerPost` is enabled
- `maxCommunitiesCount`: cap returned communities during community search

Set counts to `0` when you explicitly want to disable that result type.

## Sorting Guidance

Prefer:

- `new` for monitoring or recent trend checks
- `top` for best-performing content
- `hot` for currently active discussions
- `relevance` when the user prioritizes precise keyword matching

## Common Mistakes

- Using `query` instead of the actual field `searchTerms`
- Passing `withinCommunity` as just `technology` instead of `r/technology`
- Forgetting `startUrls` or `searchTerms`, which causes the Actor to fail
- Leaving `searchPosts` enabled when the user asked for comments only
