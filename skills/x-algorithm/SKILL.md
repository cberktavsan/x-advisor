---
name: x-algorithm
description: >
  This skill MUST be activated when the user mentions ANY of the following topics or phrases:
  "optimize my tweets", "analyze my X account", "improve engagement", "write a tweet",
  "score my tweet", "X algorithm tips", "Twitter strategy", "grow followers",
  "boost engagement", "tweet thread", "compose tweet", "draft tweet", "viral tweet",
  "engagement rate", "X analytics", "tweet performance", "content strategy for X",
  "tweet optimization", "algorithm hack", "Twitter growth", "tweet ideas",
  "trending topics", "niche analysis", "writing style analysis", "compare accounts",
  "tweet scoring", "post optimization", "social media strategy for X",
  "thread creation", "hook writing".
  Also activate when the user asks about X (formerly Twitter) algorithm mechanics,
  tweet ranking signals, reply vs like value, golden hour strategy, link penalty avoidance,
  hashtag effectiveness, tweet formatting best practices, how to get more retweets,
  how to go viral on X, how to write better tweets, tweet drafting assistance,
  X Premium benefits for reach, out-of-network distribution, For You feed optimization,
  tweet engagement multipliers, conversation chain value, posting frequency,
  daily tweet volume, content calendar for X, tweet scheduling strategy,
  audience growth on Twitter, follower acquisition tactics, building authority on X,
  personal branding on Twitter, tweet copywriting, social proof on X,
  how the X algorithm works, tweet reach optimization, impression boosting,
  profile visit optimization, video tweet strategy, media attachment best practices,
  quote tweet strategy, or any request involving composing, scoring, posting,
  analyzing, or optimizing content for the X/Twitter platform.
  This skill provides deep X algorithm knowledge backed by 16 ranking rules
  and real-time data from xquik MCP tools including style analysis, tweet composition,
  scoring with visual gauges, trending topic radar, account comparison, and tweet posting.
version: 1.0.0
---

# X Algorithm Advisor Skill

This skill provides X (Twitter) algorithm expertise powered by xquik MCP tools.

## When This Skill Applies

- User wants to optimize tweets for the X algorithm
- User asks about X/Twitter engagement strategy
- User wants to analyze their X writing style
- User wants to compose, score, or post tweets
- User mentions thread creation or tweet optimization
- User asks how the X algorithm ranks content
- User wants to compare accounts or analyze niches
- User asks about trending topics or content ideas
- User wants to grow followers or boost engagement
- User asks about viral tweet strategies or hook writing
- User mentions tweet scoring, drafting, or posting
- User asks about golden hour, link penalties, or hashtag rules
- User wants a content strategy or posting schedule for X
- User asks about reply value, retweet multipliers, or engagement signals

## Core Knowledge

X algorithm rules are in `references/algorithm-rules.md`. Key highlights:
- Reply = 27x more valuable than a like
- Threads get 3x more engagement
- External links reduce engagement by 50-90% (put links in first reply)
- First 30-60 minutes (golden hour) determine tweet reach
- Compose API's `contentRules`/`scorerWeights` override static rules at runtime

## xquik MCP Tools

All X data access goes through xquik MCP. See `references/xquik-api.md` for endpoints.

**Critical rules** (see `references/call-rules.md`):
1. NEVER combine free + paid API calls together
2. Call free endpoints first, save results, then try paid separately
3. On 402: keep free data, get checkout URL via `POST /api/v1/subscribe`, continue with free features

## Capabilities

| Capability | Reference |
|------------|-----------|
| Style analysis & comparison | `references/style-analysis.md` |
| Tweet & thread generation | `references/tweet-generation.md` |
| Scoring & visualization | `references/scoring-visuals.md` |
| Sending & threading | `references/tweet-posting.md` |
| Language & edge cases | `references/language-edge-cases.md` |

## Quick Actions

For simple requests (no full wizard needed):
- "Score this tweet" → `POST /api/v1/compose { step: "score", draft }` + gauge meter
- "What's trending?" → `GET /api/v1/radar` + filtered by user's niche
- "Compare my style with @X" → `GET /api/v1/styles/compare` + comparison table

## Example Interactions

See `examples/sample-interactions.md` for detailed conversation flows demonstrating the full wizard, quick tweet generation, and tweet scoring workflows.
