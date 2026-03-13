---
name: x-algorithm
description: >
  Use when the user wants to optimize, write, score, or post tweets on X (Twitter),
  analyze writing styles, grow followers, boost engagement, create threads,
  view trends, or understand how the X algorithm ranks content.
  Provides 16 algorithm rules, xquik MCP tools for style analysis, tweet composition,
  scoring, trending topics, account comparison, and tweet posting.
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
