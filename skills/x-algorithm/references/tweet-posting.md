# Tweet Posting and Thread Chaining

## Single Post

1. "Would you like me to post it?" → (a) Yes (b) Edit (c) Save as draft
2. Yes: `POST /api/v1/x/tweets { account: "@username", text }`
3. Success → show tweet ID + golden hour reminder
4. 402 → `call-rules.md`

### Golden Hour (After Every Post)
```
The first 30-60 minutes are critical!
1. Reply to responses IMMEDIATELY (150x valuable)
2. Share on other platforms
3. Write replies to others → drive traffic to your profile
4. In the first 5 minutes, ask 2-3 friends to engage
```

## Thread Chaining

1. Show all tweets → get approval
2. Sequential posting — each tweet uses the previous one's tweetId:
```
Tweet 1: POST /x/tweets { account, text: hook } → { tweetId: "111" }
Tweet 2: POST /x/tweets { account, text, reply_to_tweet_id: "111" } → { tweetId: "222" }
Tweet 3: POST /x/tweets { account, text, reply_to_tweet_id: "222" } → ...
```
3. If 402 mid-thread → report what was sent, save the rest as drafts

## Link Management (Rule 10)

When an external link is detected:
1. Warn: "50-90% engagement penalty"
2. Suggest: "Shall we move the link to the first reply?"
3. If accepted → tweet without link + link as a reply

## Edge Cases

**No connected account:** Work in draft mode, warn when posting.
**Multiple accounts:** Ask which one to use.
**280+ characters:** If Premium, use `is_note_tweet: true`; otherwise, shorten or convert to thread.
