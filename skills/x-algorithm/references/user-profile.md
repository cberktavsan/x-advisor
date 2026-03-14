# User Profile Persistence

## How It Works

The plugin stores each user's style analysis and preferences in a local file:
```
.claude/x-algorithm-advisor.local.md
```

This file:
- Is automatically read by Claude at session start
- Persists across conversations
- Is NOT synced or committed (local only, in .gitignore)
- Contains YAML frontmatter with structured data + markdown notes

## When to Save

Save/update the profile in these situations:
1. After STEP 1 (user identification) in `/x-advisor` — save username
2. After STEP 2 (goal setting) — save goal
3. After STEP 3 (niche confirmation) — save niche
4. After STEP 4 (analysis report) — save radar scores, tone, language, metrics
5. After `/x-style` analysis — save/update all analysis data
6. When user explicitly says "remember this" or "update my profile"

## How to Save

Use the Write tool to create/update `.claude/x-algorithm-advisor.local.md` with this exact format:

```markdown
---
username: "acmedev"
niche: ["Technology", "AI", "Finance"]
tone: "technical-casual"
language: "en"
tweet_language: "en"
goal: "engagement"
avg_length: 180
question_ratio: 25
cta_ratio: 10
media_ratio: 15
emoji_frequency: "low"
radar:
  engagement: 45
  consistency: 55
  diversity: 65
  authority: 60
  viral: 30
last_analyzed: "2026-03-14"
tweet_count_analyzed: 20
---

# Style Notes

- Tends to write about AI agents and developer tools
- Uses technical jargon but explains it
- Rarely uses emojis
- Strong at educational content, weak at hooks
- Prefers threads over single tweets for complex topics
```

## How to Read

At the START of every command (`/x-advisor`, `/x-tweet`, `/x-score`, `/x-trends`, `/x-style`):

```
Read file: .claude/x-algorithm-advisor.local.md
```

If the file exists → use the saved data, skip re-analysis unless user requests it.
If the file does NOT exist → proceed with fresh analysis, then save.

## When to Re-Analyze

Don't re-analyze every time. Only re-analyze when:
- User explicitly asks ("re-analyze my account", "refresh my style")
- `last_analyzed` is older than 7 days
- User changed their username
- User says their style has changed

When re-analyzing, update the existing file — don't create a new one.

## CRITICAL: Own Profile vs Target User

The saved profile is the USER'S OWN account. When the user asks to analyze, score, or compare a DIFFERENT account:
- ALWAYS use the username the user specified, NOT the saved profile username
- The saved `username` field = the user's own account (for style matching when generating tweets)
- If user says "score @burakbayir's tweets" → call API with `burakbayir`, NOT the saved username
- The saved profile is ONLY used for: style matching, tone reference, niche context when writing tweets FOR the user

## Profile Usage Across Commands

| Command | Reads Profile | Updates Profile |
|---------|--------------|-----------------|
| `/x-advisor` | Yes (skip analyzed steps) | Yes (after analysis) |
| `/x-tweet` | Yes (style matching) | No |
| `/x-score` | Yes (context for suggestions) | No |
| `/x-trends` | Yes (niche filtering) | No |
| `/x-style` | Yes (compare with saved) | Yes (overwrite with new data) |
