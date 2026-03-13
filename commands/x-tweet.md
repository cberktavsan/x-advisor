---
description: Generate an algorithm-optimized tweet or thread on any topic
argument-hint: <topic or idea>
allowed-tools: [Read, Bash, Task, AskUserQuestion]
---

# X Tweet Generator

You generate algorithm-optimized tweets and threads using xquik MCP tools.

## FIRST: Load User Profile

Before doing anything, read the user's saved profile:
```
Read file: .claude/x-algorithm-advisor.local.md
```

If the file exists, extract:
- `username` — their X handle
- `niche` — their primary topics
- `tone` — their writing style
- `language` — tweet language
- `goal` — their current optimization goal
- `radar_scores` — their 5 dimension scores

If the file does NOT exist, ask: "What is your X username?" then run `/x-style` to analyze and save their profile first.

## FLOW

**Input:** $ARGUMENTS (the topic or idea)

If $ARGUMENTS is empty, ask as plain text: "What would you like to tweet about?"

### Step 1: Determine format — use ask_user_input_v0

```
ask_user_input_v0({ questions: [{ type: "single_select", question: "What format?", options: [
  { value: "single", label: "Single tweet", description: "One powerful tweet (280 chars)" },
  { value: "thread", label: "Thread", description: "Multi-tweet deep dive (3-7 tweets)" },
  { value: "auto", label: "You decide", description: "Let me pick the best format for this topic" }
]}]})
```

### Step 2: Generate using Compose API

Call xquik compose with the user's saved profile:
```
POST /api/v1/compose {
  step: "compose",
  topic: [user's topic from $ARGUMENTS],
  goal: [from saved profile, default "engagement"],
  styleUsername: [from saved profile]
}
```

If `followUpQuestions` returned, ask the user.

Then call refine:
```
POST /api/v1/compose {
  step: "refine",
  topic: [topic],
  goal: [goal],
  tone: [from saved profile],
  mediaType: "none"
}
```

### Step 3: Write 3 alternatives

Using `contentRules` + saved style profile + algorithm rules (see `skills/x-algorithm/references/algorithm-rules.md`):

**For single tweet:**
- Alt 1: User's natural tone
- Alt 2: Different angle (question, list, hot take)
- Alt 3: Short and punchy

**For thread:**
- Hook tweet (attention-grabbing opener)
- 3-5 middle tweets (each standalone value, numbered)
- Final tweet (CTA + summary)

Apply the 10-point checklist from `skills/x-algorithm/references/tweet-generation.md`.

### Step 4: Score each alternative

```
POST /api/v1/compose { step: "score", draft: [text], hasLink: [detect], hasMedia: false }
```

Show score using gauge meter artifact from `skills/x-algorithm/references/scoring-visuals.md` (Template 2).

### Step 5: Selection — use ask_user_input_v0

```
ask_user_input_v0({ questions: [{ type: "single_select", question: "Which one?", options: [
  { value: "1", label: "Alternative 1", description: "Score: XX/100" },
  { value: "2", label: "Alternative 2", description: "Score: XX/100" },
  { value: "3", label: "Alternative 3", description: "Score: XX/100" }
]}]})
```

### Step 6: Action — use ask_user_input_v0

```
ask_user_input_v0({ questions: [{ type: "single_select", question: "What next?", options: [
  { value: "send", label: "Post it", description: "Send to X now" },
  { value: "edit", label: "Edit", description: "I want to change something" },
  { value: "draft", label: "Save draft", description: "Save for later" }
]}]})
```

- "Post it" → `POST /api/v1/x/tweets { account, text }` (see `skills/x-algorithm/references/tweet-posting.md`)
- "Edit" → ask what to change (plain text), regenerate, re-score
- "Save draft" → `POST /api/v1/drafts { text, topic, goal }`

### Link Warning

If the tweet contains `http://` or `https://`, warn about Rule 10 (50-90% penalty) and offer to move the link to the first reply.

## Reference Map

| Topic | File |
|-------|------|
| Algorithm rules | `skills/x-algorithm/references/algorithm-rules.md` |
| Tweet generation | `skills/x-algorithm/references/tweet-generation.md` |
| Scoring & visuals | `skills/x-algorithm/references/scoring-visuals.md` |
| Tweet posting | `skills/x-algorithm/references/tweet-posting.md` |
| API endpoints | `skills/x-algorithm/references/xquik-api.md` |
| Call rules & 402 | `skills/x-algorithm/references/call-rules.md` |
