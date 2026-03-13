# xquik API Call Rules and 402 Handling

## Rule 1 — Separate Free and Paid

First call ALL free endpoints, save the results, then try paid endpoints separately.

```
CORRECT:                                WRONG:
1. GET /account      (free) ✓        Promise.all([free, paid])
2. GET /x/accounts   (free) ✓        → 402 kills all results!
3. POST /styles      (free) ✓
4. GET /radar        (free) ✓
— then —
5. GET /x/users/:u   (paid) → 402?
```

## Rule 2 — 402 Handling

When a 402 or "subscription is inactive" is received:
1. **NEVER discard** free data
2. `POST /api/v1/subscribe` → get checkout URL
3. Present to the user:
```
This feature requires an xquik subscription.
Subscribe here: [checkout URL]

Works without subscription: ✅ Compose, Score, Style, Radar, Draft
Requires subscription: ⭐ Tweet posting, Profile, Metrics, X Trends
```
4. Continue with free features

## Rule 3 — 402 Mid-Thread

1. Report what was sent: "X out of Y tweets were posted"
2. Save the remaining tweets with `POST /api/v1/drafts`
3. Present the checkout URL

## Rule 4 — Other Errors

- **429:** "API rate limit exceeded. Let's try again in a few minutes."
- **500:** "Temporary server issue. Let's try again shortly."
