# xquik API — Complete Endpoint Reference (81 endpoints)

All calls are made through the xquik MCP tool. For call ordering rules, see `call-rules.md`.

Legend: **F** = Free · **P** = Paid (subscription required)

---

## Account (7 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/account` | Account info + subscription status | — |
| F | PATCH | `/api/v1/account` | Update account settings | body: `locale` (req) |
| F | PUT | `/api/v1/account/x-identity` | Set linked X username | body: `username` (req) |
| F | GET | `/api/v1/api-keys` | List all API keys | — |
| F | POST | `/api/v1/api-keys` | Create a new API key | body: `name` (opt) |
| F | DELETE | `/api/v1/api-keys/:id` | Revoke an API key | path: `id` |
| F | POST | `/api/v1/subscribe` | Get Stripe checkout/billing URL | — |

---

## Composition (13 endpoints)

### Compose API (3-step workflow)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | POST | `/api/v1/compose` | Compose, refine, or score a tweet | body: `step` (req), `topic`, `goal`, `draft`, `tone`, `styleUsername`, `additionalContext`, `callToAction`, `mediaType`, `hasLink`, `hasMedia` |

**Step details:**
- **compose:** `{ step: "compose", topic, goal: "engagement|followers|authority|conversation", styleUsername }` → `{ contentRules, scorerWeights, followUpQuestions }`
- **refine:** `{ step: "refine", topic, goal, tone: "casual|formal|technical|humorous", additionalContext?, callToAction?, mediaType: "photo|video|none" }` → `{ refinedRules, suggestions }`
- **score:** `{ step: "score", draft, hasLink: bool, hasMedia: bool }` → `{ score, breakdown, suggestions }`

### Drafts

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/drafts` | List saved drafts | query: `limit`, `afterCursor` |
| F | POST | `/api/v1/drafts` | Save a new draft | body: `text` (req), `topic`, `goal` |
| F | GET | `/api/v1/drafts/:id` | Get a single draft | path: `id` |
| F | DELETE | `/api/v1/drafts/:id` | Delete a draft | path: `id` |

### Styles

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/styles` | List all cached style profiles | — |
| F | POST | `/api/v1/styles` | Analyze and cache a writing style | body: `username` (req) |
| F | GET | `/api/v1/styles/:username` | Get a cached style profile | path: `username` |
| F | PUT | `/api/v1/styles/:username` | Create/update style with custom tweets | path: `username`, body: `label` (req), `tweets` (req, array) |
| F | DELETE | `/api/v1/styles/:username` | Delete a cached style profile | path: `username` |
| P | GET | `/api/v1/styles/:username/performance` | Engagement metrics for cached tweets | path: `username` |
| F | GET | `/api/v1/styles/compare` | Compare two style profiles | query: `username1` (req), `username2` (req) |

### Radar

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/radar` | Trending topics from curated sources | query: `category`, `count`, `hours`, `region`, `source` |

---

## X Accounts (5 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/x/accounts` | List connected X accounts | — |
| F | POST | `/api/v1/x/accounts` | Connect an X account | body: `username` (req), `email` (req), `password` (req), `totp_secret` (opt) |
| F | GET | `/api/v1/x/accounts/:id` | Get X account details | path: `id` |
| F | DELETE | `/api/v1/x/accounts/:id` | Disconnect X account | path: `id` |
| F | POST | `/api/v1/x/accounts/:id/reauth` | Re-authenticate X account | path: `id`, body: `password` (req), `totp_secret` (opt) |

---

## X Read (5 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/x/tweets/:tweetId` | Look up a single tweet + metrics | path: `tweetId` |
| P | GET | `/api/v1/x/tweets/search` | Search tweets by query | query: `q` (req), `limit` (opt, max 200) |
| P | GET | `/api/v1/x/users/:username` | Get X user profile | path: `username` |
| P | GET | `/api/v1/x/followers/check` | Check follow relationship | query: `source` (req), `target` (req) |
| P | GET | `/api/v1/trends` | X trending topics | query: `woeid`, `count` |

---

## X Write (16 endpoints)

All write actions require the `account` parameter (X username, e.g. `"@myaccount"`).

### Tweets

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | POST | `/api/v1/x/tweets` | Create tweet | body: `account` (req), `text` (req), `reply_to_tweet_id`, `attachment_url`, `community_id`, `is_note_tweet`, `media_ids` |
| P | DELETE | `/api/v1/x/tweets/:id` | Delete tweet | path: `id`, body: `account` |

### Engagement

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | POST | `/api/v1/x/tweets/:id/like` | Like a tweet | path: `id`, body: `account` |
| P | DELETE | `/api/v1/x/tweets/:id/like` | Unlike a tweet | path: `id`, body: `account` |
| P | POST | `/api/v1/x/tweets/:id/retweet` | Retweet | path: `id`, body: `account` |

### Social

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | POST | `/api/v1/x/users/:id/follow` | Follow user (numeric ID) | path: `id`, body: `account` |
| P | DELETE | `/api/v1/x/users/:id/follow` | Unfollow user | path: `id`, body: `account` |
| P | POST | `/api/v1/x/dm/:userId` | Send DM | path: `userId`, body: `account`, `text` (req), `media_ids`, `reply_to_message_id` |

### Media

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | POST | `/api/v1/x/media` | Upload media (file or URL) | body: `account` (req), `file` or `url`, `is_long_video` |
| P | POST | `/api/v1/x/media/download` | Download media from tweets | body: `tweetInput` or `tweetIds` (array, max 50) |

### Profile

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | PATCH | `/api/v1/x/profile` | Update profile | body: `account`, `name`, `description`, `location`, `url` |
| P | PATCH | `/api/v1/x/profile/avatar` | Update avatar | body: `account`, `file` or `url` |
| P | PATCH | `/api/v1/x/profile/banner` | Update banner | body: `account`, `file` or `url` |

### Communities

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | POST | `/api/v1/x/communities` | Create community | body: `account`, `name` (req), `description` |
| P | DELETE | `/api/v1/x/communities/:id` | Delete community | path: `id`, body: `account`, `community_name` (req) |
| P | POST | `/api/v1/x/communities/:id/join` | Join community | path: `id`, body: `account` |
| P | DELETE | `/api/v1/x/communities/:id/join` | Leave community | path: `id`, body: `account` |

---

## Extractions (5 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/extractions` | List extraction jobs | query: `limit`, `after`, `toolType`, `status` |
| P | POST | `/api/v1/extractions` | Start a new extraction | body: `toolType` (req), `targetUsername`, `targetTweetId`, `searchQuery`, `resultsLimit`, `fromUser`, `toUser`, `mentioning`, `language`, `sinceDate`, `untilDate`, `mediaType`, `minFaves`, `minRetweets`, `minReplies`, `verifiedOnly`, `replies`, `retweets` |
| P | POST | `/api/v1/extractions/estimate` | Estimate extraction cost | body: same as start |
| P | GET | `/api/v1/extractions/:id` | Get job details + results | path: `id`, query: `limit`, `after` |
| P | GET | `/api/v1/extractions/:id/export` | Export results (CSV/XLSX/MD) | path: `id`, query: `format` |

---

## Draws / Giveaways (4 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/draws` | List giveaway draws | query: `limit`, `after` |
| P | POST | `/api/v1/draws` | Run a giveaway draw | body: `tweetUrl` (req), `winnerCount`, `filters` |
| P | GET | `/api/v1/draws/:id` | Get draw details + winners | path: `id` |
| P | GET | `/api/v1/draws/:id/export` | Export draw results | path: `id`, query: `format` |

---

## Monitors (5 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/monitors` | List all monitors | — |
| P | POST | `/api/v1/monitors` | Create a monitor | body: `username` (req), `eventTypes` (req): `tweet.new`, `tweet.reply`, `tweet.quote`, `tweet.retweet`, `follower.gained`, `follower.lost` |
| P | GET | `/api/v1/monitors/:id` | Get monitor details | path: `id` |
| P | PATCH | `/api/v1/monitors/:id` | Update monitor | path: `id`, body: `isActive`, `eventTypes` |
| P | DELETE | `/api/v1/monitors/:id` | Delete monitor | path: `id` |

---

## Events (2 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/events` | List stream events | query: `limit`, `after`, `monitorId`, `eventType` |
| P | GET | `/api/v1/events/:id` | Get a single event | path: `id` |

---

## Webhooks (6 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/webhooks` | List all webhooks | — |
| P | POST | `/api/v1/webhooks` | Create a webhook | body: `url` (req), `eventTypes` (req) |
| P | PATCH | `/api/v1/webhooks/:id` | Update webhook | path: `id`, body: `url`, `eventTypes`, `isActive` |
| P | DELETE | `/api/v1/webhooks/:id` | Deactivate webhook | path: `id` |
| P | GET | `/api/v1/webhooks/:id/deliveries` | List deliveries | path: `id` |
| P | POST | `/api/v1/webhooks/:id/test` | Send test event | path: `id` |

---

## Trends (1 endpoint)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| P | GET | `/api/v1/trending/:source` | Trending by source | path: `source` (`reddit`, `github`, `hacker-news`, `google-trends`, `wikipedia`, `startups`, `polymarket`), query: `count` |

---

## Bot / Platform Links (4 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | POST | `/api/v1/bot/platform-links` | Link platform user to xquik | body: `platform` (req), `platformUserId` (req) |
| F | DELETE | `/api/v1/bot/platform-links` | Unlink platform user | body: `platform`, `platformUserId` |
| F | GET | `/api/v1/bot/platform-links/lookup` | Look up user by platform ID | query: `platform`, `platformUserId` |
| F | POST | `/api/v1/bot/usage` | Track bot token usage | body: `platformUserId`, `inputTokens`, `outputTokens` |

---

## Integrations (7 endpoints)

| | Method | Endpoint | Purpose | Key Parameters |
|---|---|---|---|---|
| F | GET | `/api/v1/integrations` | List all integrations | — |
| F | POST | `/api/v1/integrations` | Create integration | body: `type` (req), `name` (req), `config` (req), `eventTypes` (req) |
| F | GET | `/api/v1/integrations/:id` | Get integration details | path: `id` |
| F | PATCH | `/api/v1/integrations/:id` | Update integration | path: `id`, body: `name`, `eventTypes`, `isActive`, `silentPush` |
| F | DELETE | `/api/v1/integrations/:id` | Delete integration | path: `id` |
| F | GET | `/api/v1/integrations/:id/deliveries` | List delivery history | path: `id`, query: `limit` |
| F | POST | `/api/v1/integrations/:id/test` | Send test delivery | path: `id` |

---

## Summary

| Category | Free | Paid | Total |
|----------|------|------|-------|
| Account | 7 | 0 | 7 |
| Composition | 12 | 1 | 13 |
| X Accounts | 5 | 0 | 5 |
| X Read | 0 | 5 | 5 |
| X Write | 0 | 16 | 16 |
| Extractions | 0 | 5 | 5 |
| Draws | 0 | 4 | 4 |
| Monitors | 0 | 5 | 5 |
| Events | 0 | 2 | 2 |
| Webhooks | 0 | 6 | 6 |
| Trends | 0 | 1 | 1 |
| Bot | 4 | 0 | 4 |
| Integrations | 7 | 0 | 7 |
| **Total** | **35** | **46** | **81** |

### Compose ≠ Send
- "write/create/draft a tweet" → `POST /api/v1/compose` (free)
- "send/post/publish a tweet" → `POST /api/v1/x/tweets` (paid)
- User has ready text and wants to post → NEVER use compose, go directly to `/x/tweets`
