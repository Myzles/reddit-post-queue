# reddit-post-queue

Posts waiting to be published by the **agent-post-relay** Reddit app (built on Reddit's Developer Platform, Devvit).

The app is installed in communities its owner moderates. Every 5 minutes it reads `queue.json`, and posts ready items
for its own community from its labeled app account, within the daily cap and spacing the moderators set.
Items for other communities are ignored.

## queue.json

```json
{
  "version": 1,
  "posts": [
    {
      "id": "2026-11-18-devlog-1",
      "subreddit": "ExampleCommunity",
      "title": "Devlog #1",
      "text": "Markdown body",
      "flairText": "Devlog",
      "notBefore": "2026-11-18T17:00:00Z"
    }
  ]
}
```

| Field | Required | Notes |
|---|---|---|
| `id` | yes | Unique and never reused. Posted ids are remembered, so editing a posted item does nothing. |
| `subreddit` | yes | Community name without `r/`. |
| `title` | yes | Up to 300 characters. |
| `text` or `url` | one of them | Markdown body for a text post, or an `https://` link for a link post. |
| `flairId`, `flairText` | no | Post flair. |
| `nsfw`, `spoiler` | no | `true` / `false`. |
| `notBefore` | no | ISO 8601 time; the item waits until then. |

Posted items can be removed from the file later; the app keeps its own record.
