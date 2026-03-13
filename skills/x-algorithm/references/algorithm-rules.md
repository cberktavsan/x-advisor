# X Algorithm Knowledge Base — 16 Rules

Compiled from X's open-source ranking algorithm and 2024-2026 research.

## Technical Rules

**Rule 1 — Candidate Isolation:** Each tweet is scored independently. Account-level reputation has an indirect effect.

**Rule 2 — Engagement Prediction Model:** The algorithm generates probability predictions for 15+ action types.

**Rule 3 — Positive Signal Weights (like = 1x):**
| Signal | Multiplier |
|--------|------------|
| Fav (like) | 1x |
| Reply | 27x |
| Retweet | 20x |
| Quote tweet | 25x |
| Video view (2s+) | 10x |
| Profile visit | 12x |

**Rule 4 — Negative Signals:** Block, mute, report carry heavy penalties. A single block erases dozens of likes.

**Rule 5 — Final Score:** `Σ(weight_i × P(action_i))`

**Rule 6 — Two Layers:** In-network (follower timeline) + out-of-network ("For You" viral distribution).

## Current Best Practices

**Rule 7 — Reply:** 27x valuable, conversation chain 150x. Write meaningful replies to others.

**Rule 8 — Thread:** 3x more engagement. Each tweet should provide standalone value (Rule 1).

**Rule 9 — Video:** 10x engagement. 2s+ watch time = view signal.

**Rule 10 — Link Penalty:** External links cause a 50-90% drop. Solution: put the link in the first reply.

**Rule 11 — Golden Hour:** Engagement velocity in the first 30-60 minutes is critical. Multiplies reach.

**Rule 12 — Hashtags:** Nearly ineffective. 3+ can be harmful.

**Rule 13 — Premium:** In-network 4x, out-of-network 2x boost.

**Rule 14 — Daily Volume:** 2-5 tweets is the sweet spot.

**Rule 15 — Consistency > Virality:** Regular posting is more valuable.

**Rule 16 — Runtime:** `contentRules`/`scorerWeights` returned from the Compose API update this baseline. API data takes priority.

## Goal-Based Strategy

| Goal | Priority Rules | Tactic |
|------|---------------|--------|
| Grow followers | 6, 8, 15 | Thread + educational content + consistent posting |
| Boost engagement | 7, 9, 11 | Ask questions + add media + golden hour |
| Build authority | 1, 5, 8 | Data-backed thread + quote tweet |
| Start conversations | 7, 3 | Open-ended question + controversial opinion |
