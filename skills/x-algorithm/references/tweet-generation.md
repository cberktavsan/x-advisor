# Tweet and Thread Generation

Follow the rules in `algorithm-rules.md` when writing tweets.

## Single Tweet

**F1 — Compose:** `POST /api/v1/compose { step: "compose", topic, goal, styleUsername }`
**F2 — Follow-up:** If the API returns `followUpQuestions`, ask the user.
**F3 — Refine:** `POST /api/v1/compose { step: "refine", topic, goal, tone, additionalContext?, callToAction?, mediaType? }`

**F4 — Write 3 Alternatives:**
- Alt 1: Primary tone (from style)
- Alt 2: Different approach (question, list, provocation)
- Alt 3: Shorter/punchier

**Checklist (for each tweet):**
1. Does it trigger replies? (Rule 7: 27x)
2. Is it ready for golden hour? (Rule 11)
3. Contains an external link? → move to reply (Rule 10)
4. 3+ hashtags? → remove them (Rule 12)
5. Can a media suggestion be made? (Rule 9: 10x)
6. Does it match the style?
7. Any negative signal risk? (Rule 4)
8. Does it provide standalone value? (Rule 1)
9. Does it have a CTA?
10. Is it within 280 characters?

**F5 — Score:** `POST /api/v1/compose { step: "score", draft, hasLink, hasMedia }` → gauge meter (`scoring-visuals.md`)
**F6 — Select:** Present 3 alternatives with scores → after selection, go to `tweet-posting.md`

## Thread

**Structure:** Hook → middle tweets (each standalone) → CTA + summary. Ideal: 3-7 tweets.

**Hook techniques:**
- Surprising data: "A reply is 27x more valuable. But most people don't know this."
- Contrast: "Writing a tweet is easy. Writing a tweet the algorithm loves is science."
- Question: "Why do some tweets get seen by thousands?"
- List promise: "5 rules to grow on X"

**Middle tweets:** Standalone value, numbered, an aha moment in each tweet, no transition sentences.

**Final tweet:** Summary + CTA ("Found this useful? RT!" / "What do you think?" / "Follow for more").

**Scoring:** Score each tweet individually → present average + min + max.
