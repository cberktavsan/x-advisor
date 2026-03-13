# Style Analysis and Comparison

## Analysis Flow

1. `POST /api/v1/styles { username }` → tweet array
2. Analyze:

**Language:** Majority language = primary. If 30%+ second language exists, ask the user.

**Niche:** Extract topic frequencies (Technology, AI, Finance, Crypto, Marketing, Education, Lifestyle, etc). Top 3 = primary niche.

**Style profile:** Avg. length, emoji frequency, question ratio, CTA ratio, media ratio, tone (`formal|casual|technical|humorous|inspirational|controversial`).

**Top tweets (paid):** `GET /api/v1/styles/:username/performance` → top 3 tweets by likes/replies/RTs each.

## Radar Dimension Calculation (0-100)

| Dimension | Calculation |
|-----------|-------------|
| Engagement | Avg. interactions per tweet / followers × 10000. If no paid data, estimate from question+CTA ratio |
| Consistency | Standard deviation of tweet intervals. Low deviation = high score. Daily 2-5 = high |
| Diversity | Number of different niches + formats (text/question/list/media/thread). 3-5 balanced topics = high |
| Authority | Educational tweet × 30 + thread × 20 + quote tweet × 15 + tone consistency × 10 |
| Viral | First 50 char attention factor + shareable format + ratio of tweets with strong emotion |

For visuals → `scoring-visuals.md` (radar chart template).

## Comparison Flow

1. Ask for target username
2. `POST /api/v1/styles { username: target }` (if not in cache)
3. `GET /api/v1/styles/compare?username1=X&username2=Y`
4. Show comparison table (see: `scoring-visuals.md`)
5. Present strengths + areas for improvement

## Few Tweets (<5)

Offer 3 paths:
1. "Is there an account you're inspired by? I can analyze that one."
2. "Describe your style: what's your tone? What are your topics?"
3. "Paste tweets you like." → `PUT /api/v1/styles/:username { label, tweets: [{text}] }`
