# xquik API Endpoint Reference

All calls are made through the xquik MCP tool. For call ordering, see `call-rules.md`.

## Free Endpoints

| Endpoint | Method | Purpose | Parameters |
|---|---|---|---|
| `/api/v1/account` | GET | Account + subscription status | — |
| `/api/v1/x/accounts` | GET | Connected X accounts | — |
| `/api/v1/styles` | POST | Start style analysis | body: `{ username }` |
| `/api/v1/styles` | GET | Cached styles | — |
| `/api/v1/styles/:username` | GET | Get style profile | path: `username` |
| `/api/v1/styles/:username` | PUT | Create manual style | body: `{ label, tweets: [{text}] }` |
| `/api/v1/styles/compare` | GET | Compare two styles | query: `username1`, `username2` |
| `/api/v1/compose` | POST | Compose/refine/score (3 steps) | body: see below |
| `/api/v1/drafts` | POST | Save draft | body: `{ text, topic?, goal? }` |
| `/api/v1/drafts` | GET | List drafts | query: `limit`, `afterCursor` |
| `/api/v1/radar` | GET | Trending topics | query: `category`, `count`, `hours`, `region`, `source` |
| `/api/v1/subscribe` | POST | Stripe checkout URL | — |

### Compose API (3 Steps)

**compose:** `{ step: "compose", topic, goal: "engagement|followers|authority|conversation", styleUsername }`
→ `{ contentRules, scorerWeights, followUpQuestions }`

**refine:** `{ step: "refine", topic, goal, tone: "casual|formal|technical|humorous", additionalContext?, callToAction?, mediaType: "photo|video|none" }`
→ `{ refinedRules, suggestions }`

**score:** `{ step: "score", draft, hasLink: bool, hasMedia: bool }`
→ `{ score, breakdown, suggestions }`

## Paid Endpoints

| Endpoint | Method | Purpose | Parameters |
|---|---|---|---|
| `/api/v1/x/users/:username` | GET | Profile details | path: `username` |
| `/api/v1/x/tweets/search` | GET | Tweet search | query: `q`, `limit` (max 200) |
| `/api/v1/x/tweets/:tweetId` | GET | Tweet + metrics | path: `tweetId` |
| `/api/v1/x/tweets` | POST | Post tweet | body: `{ account, text, reply_to_tweet_id?, media_ids?, is_note_tweet? }` |
| `/api/v1/x/tweets/:id` | DELETE | Delete tweet | body: `{ account }` |
| `/api/v1/styles/:username/performance` | GET | Engagement metrics | path: `username` |
| `/api/v1/trends` | GET | X trending | query: `woeid`, `count` |
| `/api/v1/x/media` | POST | Upload media | body: `{ account, url }` |

### Compose ≠ Send
- "write/create/draft a tweet" → `POST /api/v1/compose` (free)
- "send/post/publish a tweet" → `POST /api/v1/x/tweets` (paid)
