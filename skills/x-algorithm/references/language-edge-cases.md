# Language Management and Edge Cases

## Language

- **Interface language:** The language of the user's first message. Visual labels and wizard text use this language.
- **Tweet language:** The primary language detected from style analysis. Tweet content uses this language.
- **Mixed:** If 30%+ second language exists, ask the user.
- Example: User speaks Turkish + tweets in English → interface TR, tweets EN.

## Thread vs Single

- **Suggest thread:** Complex topic, tutorial, 5+ item list, story
- **Suggest single:** Short opinion, question, joke, announcement
- Unclear → ask

## Trend Presentation

After `GET /api/v1/radar`:
- Highlight trends that match the user's niche
- List 5-10 trends
- Ask "Which topic would you like to write a tweet about?"

## Existing Tweet Scoring

1. Ask for the tweet text
2. `POST /api/v1/compose { step: "score", draft, hasLink, hasMedia }`
3. Show gauge meter
4. Provide specific suggestions for low-scoring areas
5. Create an improved version + score again
