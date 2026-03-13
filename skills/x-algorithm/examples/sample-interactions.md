# Sample Interactions

Three example conversations showing the X Algorithm Advisor in action.

---

## Example 1: Full Wizard Flow

A complete walkthrough from account setup through style analysis, goal selection, tweet generation, and posting.

---

**User:** /x-advisor

**Agent:**

*[Calls `GET /api/v1/account` and `GET /api/v1/x/accounts` via xquik MCP]*

*[Both return 200 OK. Account active, connected X account: @alexbuilds]*

Welcome to the **X Algorithm Advisor**! Here is your account status:

| Item | Status |
|------|--------|
| xquik Account | Active |
| Connected X Account | @alexbuilds |
| Subscription | Free Plan |

Let me analyze your writing style to give you personalized recommendations.

*[Calls `POST /api/v1/styles { username: "alexbuilds" }` via xquik MCP]*

*[Returns 24 tweets. Primary language: English. Niches detected: AI (42%), Startups (31%), Productivity (27%)]*

Here is your **Style Profile**:

*[Renders radar chart artifact with X-themed dark UI]*

**Style Profile -- @alexbuilds**

| Dimension | Score |
|-----------|-------|
| Engagement | 62 |
| Consistency | 45 |
| Diversity | 71 |
| Authority | 58 |
| Viral | 39 |

**Niche Distribution:**
- AI / Machine Learning: 42%
- Startups / Entrepreneurship: 31%
- Productivity: 27%

**Style Notes:**
- Tone: Casual-technical blend
- Avg. tweet length: 187 characters
- Question ratio: 18% (good for engagement)
- Media usage: 12% (room for improvement -- media gives 10x signal)
- Emoji frequency: Low
- CTA ratio: 8% (could be higher)

**Key Observations:**
1. Your Viral score (39) is your weakest area. Your opening lines could be stronger hooks.
2. Consistency at 45 suggests irregular posting. The algorithm rewards 2-5 tweets daily.
3. Your Diversity is strong at 71 -- you cover multiple topics without being scattered.

Now, what is your primary goal?

1. **Grow followers** -- Thread-first strategy with educational content
2. **Boost engagement** -- Question-driven tweets + media + golden hour tactics
3. **Build authority** -- Data-backed threads and quote tweets
4. **Start conversations** -- Open-ended questions + thought-provoking takes

**User:** 2 -- boost engagement

**Agent:**

Great choice. Let me get the latest algorithm guidance and compose tweets tailored to your engagement goal.

*[Calls `POST /api/v1/compose { step: "compose", topic: "AI", goal: "engagement", styleUsername: "alexbuilds" }` via xquik MCP]*

*[Returns contentRules, scorerWeights, and followUpQuestions: ["Any specific AI topic?", "Prefer a hot take or educational angle?"]]*

The algorithm has a couple of questions to help me dial in:

1. Is there a specific AI topic you want to focus on? (e.g., AI agents, LLMs, AI in startups)
2. Do you prefer a hot take or an educational angle?

**User:** AI agents replacing SaaS. Hot take.

**Agent:**

*[Calls `POST /api/v1/compose { step: "refine", topic: "AI agents replacing SaaS", goal: "engagement", tone: "casual", additionalContext: "hot take angle", callToAction: "question", mediaType: "none" }` via xquik MCP]*

Here are 3 alternatives. Each one follows the algorithm rules -- designed to trigger replies (27x value), avoid link penalties, and work within golden hour dynamics.

---

**Alternative 1 -- Direct Hot Take** (your natural tone)

> Most SaaS products will be dead in 3 years.
>
> Not because they are bad. Because AI agents will do the same job for $0 and no UI.
>
> The SaaS founders who survive? The ones rebuilding as agent-first platforms right now.
>
> What SaaS tool do you think gets replaced first?

*[Calls `POST /api/v1/compose { step: "score", draft: "...", hasLink: false, hasMedia: false }` via xquik MCP]*

*[Renders gauge meter artifact: Score 78, green]*

**Score: 78/100**
- Reply trigger: Strong (ends with direct question) +20
- Standalone value: Strong (clear thesis) +18
- Hook strength: Strong (bold claim in first line) +16
- No link penalty: +10
- Golden hour ready: Yes +8
- Media suggestion: Adding an image comparing SaaS vs Agent costs could push this to 85+

---

**Alternative 2 -- List Format**

> 5 SaaS categories AI agents will kill by 2028:
>
> 1. Basic CRMs -- agents remember everything
> 2. Scheduling tools -- agents negotiate calendars
> 3. Email marketing -- agents write + send + optimize
> 4. Data entry tools -- agents see + act
> 5. Simple analytics -- agents surface insights on their own
>
> Which one goes first?

*[Score: 74/100]*

**Score: 74/100**
- Reply trigger: Strong +18
- Scannable format: List structure aids engagement +15
- Hook strength: Moderate (list promise) +14
- Standalone value: Each item gives value +12

---

**Alternative 3 -- Short and Punchy**

> SaaS companies charge you $29/month for a dashboard.
>
> AI agents will do the same thing by reading your data and just telling you the answer.
>
> The entire UI layer is about to become irrelevant.

*[Score: 68/100]*

**Score: 68/100**
- Hook strength: Strong (relatable pain point) +16
- Standalone value: Good +14
- Reply trigger: Weaker (no explicit question) +8
- Suggestion: Adding "Agree or disagree?" at the end would boost reply potential by +10

---

Which alternative would you like to go with? I can also mix elements from multiple options.

**User:** I like #1. Let's go with that.

**Agent:**

Great pick -- it scored the highest at 78/100. Ready to post?

> Most SaaS products will be dead in 3 years.
>
> Not because they are bad. Because AI agents will do the same job for $0 and no UI.
>
> The SaaS founders who survive? The ones rebuilding as agent-first platforms right now.
>
> What SaaS tool do you think gets replaced first?

Options:
1. **Post now** to @alexbuilds
2. **Edit** before posting
3. **Save as draft** for later

**User:** Post it!

**Agent:**

*[Calls `POST /api/v1/x/tweets { account: "@alexbuilds", text: "Most SaaS products will be dead in 3 years.\n\nNot because they are bad. Because AI agents will do the same job for $0 and no UI.\n\nThe SaaS founders who survive? The ones rebuilding as agent-first platforms right now.\n\nWhat SaaS tool do you think gets replaced first?" }` via xquik MCP]*

*[Returns 200 OK, tweetId: "1901234567890"]*

Posted successfully! Tweet ID: 1901234567890

**Golden Hour Checklist -- the next 30-60 minutes are critical:**

1. Reply to every response IMMEDIATELY (conversation chains are 150x valuable)
2. Share the tweet on LinkedIn / Discord / Slack communities
3. Write 2-3 thoughtful replies to other accounts in the AI niche to drive profile visits
4. Ask 2-3 friends to engage within the first 5 minutes

Good luck with the golden hour!

---

## Example 2: Quick Tweet Generation

A fast flow when the user provides a topic directly -- no full wizard needed.

---

**User:** /x-advisor AI agents and the future

**Agent:**

*[Calls `GET /api/v1/account` and `GET /api/v1/x/accounts` via xquik MCP]*

*[Both return 200 OK. Connected account: @sarahcodes. Calls `GET /api/v1/styles/sarahcodes` -- cached style exists.]*

I found your existing style profile for **@sarahcodes**. Skipping analysis and jumping straight to tweet generation.

**Your style snapshot:** Technical-casual tone, primary niche: AI/Dev Tools, avg. length: 210 chars, strong hook game.

*[Calls `POST /api/v1/compose { step: "compose", topic: "AI agents and the future", goal: "engagement", styleUsername: "sarahcodes" }` via xquik MCP]*

*[Calls `POST /api/v1/compose { step: "refine", topic: "AI agents and the future", goal: "engagement", tone: "casual", mediaType: "none" }` via xquik MCP]*

Here are 3 tweet options on "AI agents and the future":

---

**Alternative 1 -- Bold Prediction**

> We are about to mass-produce junior employees.
>
> AI agents that can browse, code, email, and make decisions.
>
> The question is not whether they will replace jobs. It is which NEW jobs they create that we cannot even imagine yet.

*[Calls `POST /api/v1/compose { step: "score", draft: "...", hasLink: false, hasMedia: false }` via xquik MCP]*

*[Renders gauge meter artifact: Score 72, green]*

**Score: 72/100**

---

**Alternative 2 -- Provocative Question**

> If an AI agent can do 80% of a knowledge worker's job at 1% of the cost...
>
> What exactly are we paying humans for?
>
> (Hint: it is the 20% that requires judgment, empathy, and creative risk-taking)

*[Score: 81/100]*

*[Renders gauge meter artifact: Score 81, green]*

**Score: 81/100** -- Highest score. The open question format is strong for reply generation.

---

**Alternative 3 -- Short and Viral**

> Hot take: The best AI agents will not be the smartest ones.
>
> They will be the ones that know when to ask a human for help.

*[Score: 69/100]*

*[Renders gauge meter artifact: Score 69, yellow]*

**Score: 69/100** -- Punchy and shareable, but lacks a reply trigger. Adding "What do you think?" would push it past 75.

---

My recommendation: **Alternative 2** scored highest at 81. The question format aligns with Rule 7 (replies = 27x value) and your style naturally leans toward thought-provoking questions.

What would you like to do?
1. **Post** one of these now
2. **Edit** a specific alternative
3. **Save as draft**

**User:** Save #2 as draft

**Agent:**

*[Calls `POST /api/v1/drafts { text: "If an AI agent can do 80% of a knowledge worker's job at 1% of the cost...\n\nWhat exactly are we paying humans for?\n\n(Hint: it is the 20% that requires judgment, empathy, and creative risk-taking)", topic: "AI agents and the future", goal: "engagement" }` via xquik MCP]*

*[Returns 200 OK]*

Draft saved! You can retrieve it anytime with your drafts list.

**Tip:** This tweet scored 81/100. When you are ready to post, aim for golden hour -- the first 30-60 minutes of engagement velocity determine your reach. Consider posting when your audience is most active.

---

## Example 3: Tweet Scoring

The user pastes an existing tweet for scoring, gets improvement suggestions, and sees a revised version score higher.

---

**User:** Can you score this tweet for me?

"Just launched our new AI feature! Check it out here: https://example.com/launch We've been working on this for months and I'm so excited to share it with you all! #AI #launch #startup #product #newfeature"

**Agent:**

Let me score this tweet against the X algorithm rules.

*[Calls `POST /api/v1/compose { step: "score", draft: "Just launched our new AI feature! Check it out here: https://example.com/launch We've been working on this for months and I'm so excited to share it with you all! #AI #launch #startup #product #newfeature", hasLink: true, hasMedia: false }` via xquik MCP]*

*[Renders gauge meter artifact: Score 23, red]*

**Score: 23/100**

Here is the detailed breakdown:

| Category | Score | Issue |
|----------|-------|-------|
| Link Penalty | -35 | External link in tweet body causes 50-90% reach drop (Rule 10) |
| Hashtag Penalty | -15 | 5 hashtags -- 3+ hashtags hurt distribution (Rule 12) |
| Reply Trigger | 2/20 | No question or CTA to encourage replies (Rule 7: replies = 27x) |
| Hook Strength | 5/20 | "Just launched" is generic, does not stop the scroll |
| Standalone Value | 4/15 | Does not explain WHAT the feature does or WHY it matters |
| Negative Signal Risk | Low | No controversy, but engagement will be too low to surface |
| Media | 0/10 | No media attached (Rule 9: video/image = 10x signal) |

**Specific Issues and Fixes:**

1. **External link in the body** -- This is the biggest problem. The algorithm penalizes tweets with links by 50-90%. Move the link to the first reply instead.

2. **5 hashtags** -- Hashtags are nearly ineffective on X and 3+ actively harm distribution. Remove all of them.

3. **No reply trigger** -- The tweet tells people about your launch but gives them no reason to respond. Add a question like "What would you build with it?" or "What feature should we add next?"

4. **Weak hook** -- "Just launched" is what every product announcement says. Lead with the user benefit or a surprising stat instead.

5. **No media** -- A demo GIF, screenshot, or short video would add 10x engagement signal.

Want me to create an improved version?

**User:** Yes please!

**Agent:**

Here is a rewritten version that fixes all 5 issues:

**Improved Tweet:**

> We taught an AI to read your entire codebase and suggest architecture improvements in seconds.
>
> Tested it on 50 repos. Average result: 34% fewer redundant abstractions.
>
> What is the messiest part of YOUR codebase? Reply and I will run it for free.

*[Link goes in the first reply: "Try it here: https://example.com/launch"]*

*[Calls `POST /api/v1/compose { step: "score", draft: "We taught an AI to read your entire codebase and suggest architecture improvements in seconds.\n\nTested it on 50 repos. Average result: 34% fewer redundant abstractions.\n\nWhat is the messiest part of YOUR codebase? Reply and I will run it for free.", hasLink: false, hasMedia: false }` via xquik MCP]*

*[Renders gauge meter artifact: Score 82, green]*

**Score: 82/100** (up from 23)

| Category | Before | After | Change |
|----------|--------|-------|--------|
| Link Penalty | -35 | 0 | +35 (moved to reply) |
| Hashtag Penalty | -15 | 0 | +15 (removed all) |
| Reply Trigger | 2 | 19 | +17 (direct question + incentive) |
| Hook Strength | 5 | 18 | +13 (specific + intriguing) |
| Standalone Value | 4 | 14 | +10 (concrete data point) |
| Media | 0 | 0 | -- (adding a demo GIF could push to 90+) |

**What changed and why:**

1. **Link moved to first reply** -- Eliminates the 50-90% penalty. The tweet body is now clean for the algorithm.
2. **All hashtags removed** -- Zero hashtags performs better than any number of hashtags on X.
3. **Strong reply trigger** -- "What is the messiest part of YOUR codebase?" invites personal answers. "Reply and I will run it for free" adds an incentive. Replies are worth 27x a like.
4. **Specific hook** -- "We taught an AI to read your entire codebase" is concrete and scroll-stopping, unlike "Just launched our new AI feature."
5. **Data point** -- "34% fewer redundant abstractions" gives the tweet standalone value and credibility.

**To push past 90:** Attach a 15-second screen recording showing the tool in action. Video gets a 10x engagement signal.

Would you like to:
1. **Post this** (tweet + link in first reply as a thread)
2. **Edit** the improved version
3. **Save as draft**
