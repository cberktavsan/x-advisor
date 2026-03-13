# Scoring and Visualization Templates

## CRITICAL RULES

1. NEVER write HTML/SVG visuals as inline text. Create an **artifact** for each visual.
2. ALWAYS use the EXACT templates below. Do NOT improvise or create your own HTML. Copy the template, replace ONLY the placeholder values (marked with UPPERCASE like `USERNAME`, `SCORE`, `TOPIC`), and output as an artifact.
3. ALL visuals must match the xquik brand. Never use X/Twitter dark theme, never use generic colors.

## xquik Design Tokens

```
Background:       #f5f3f0
Card:             #ffffff
Text:             #242121
Muted text:       #585455
Border:           1px solid rgba(36,33,33,0.15)
Accent (brand):   #4c2626
Teal:             #009588
Dark teal:        #104e64
Gold:             #fcbb00
Orange:           #f99c00
Red (error):      #e40014
Muted surface:    #edebe7
Radius:           10px
Heading font:     'Instrument Serif', Georgia, serif (always italic)
Body font:        'Outfit', system-ui, -apple-system, sans-serif
Score good 70+:   #009588
Score avg 40-69:  #fcbb00
Score low 0-39:   #e40014
```

---

## TEMPLATE 1 — Full Analysis Report

Use this template after style analysis (STEP 4). It includes radar chart + niche bars + key metrics in one artifact. Replace ALL placeholder values.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:#f5f3f0; font-family:'Outfit',system-ui,-apple-system,sans-serif; color:#242121; padding:20px; }
  .card { background:#fff; border:1px solid rgba(36,33,33,0.15); border-radius:10px; padding:24px; margin-bottom:16px; }
  .card-title { font-family:'Instrument Serif',Georgia,serif; font-style:italic; color:#4c2626; font-size:1.3rem; margin-bottom:4px; }
  .card-subtitle { color:#585455; font-size:13px; margin-bottom:20px; }
  .score-row { display:flex; justify-content:space-between; align-items:center; padding:12px 0; border-bottom:1px solid rgba(36,33,33,0.08); }
  .score-row:last-child { border-bottom:none; }
  .score-label { font-size:13px; color:#585455; }
  .score-value { font-size:14px; font-weight:600; }
  .bar-row { margin-bottom:14px; }
  .bar-label { display:flex; justify-content:space-between; margin-bottom:4px; }
  .bar-name { font-size:13px; color:#585455; }
  .bar-pct { font-size:13px; font-weight:600; color:#242121; }
  .bar-track { background:#edebe7; border-radius:6px; height:8px; overflow:hidden; }
  .bar-fill { height:100%; border-radius:6px; transition:width 0.3s; }
  .metrics-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; }
  .metric-item { background:#f5f3f0; border-radius:8px; padding:14px; text-align:center; }
  .metric-value { font-size:1.5rem; font-weight:700; color:#4c2626; }
  .metric-label { font-size:11px; color:#585455; margin-top:2px; }
  .badge { display:inline-block; padding:3px 10px; border-radius:20px; font-size:11px; font-weight:600; }
  .badge-good { background:rgba(0,149,136,0.12); color:#009588; }
  .badge-avg { background:rgba(252,187,0,0.15); color:#a36100; }
  .badge-low { background:rgba(228,0,20,0.1); color:#e40014; }
  .breakdown-row { display:flex; align-items:center; padding:10px 0; border-bottom:1px solid rgba(36,33,33,0.06); }
  .breakdown-row:last-child { border-bottom:none; }
  .breakdown-label { flex:1; font-size:13px; color:#585455; }
  .breakdown-bar { flex:2; margin:0 12px; background:#edebe7; border-radius:4px; height:6px; overflow:hidden; }
  .breakdown-fill { height:100%; border-radius:4px; }
  .breakdown-score { font-size:13px; font-weight:600; min-width:40px; text-align:right; }
</style>
</head>
<body>

<!-- SECTION 1: RADAR CHART -->
<div class="card" style="text-align:center">
  <div class="card-title">Style Profile</div>
  <div class="card-subtitle">@USERNAME · TWEET_COUNT tweets analyzed</div>
  <svg viewBox="0 0 300 300" style="max-width:260px;margin:0 auto;display:block">
    <polygon points="150,30 270,110 230,250 70,250 30,110" fill="none" stroke="rgba(36,33,33,0.1)" stroke-width="1"/>
    <polygon points="150,66 234,122 206,222 94,222 66,122" fill="none" stroke="rgba(36,33,33,0.07)" stroke-width="0.5"/>
    <polygon points="150,102 198,134 182,194 118,194 102,134" fill="none" stroke="rgba(36,33,33,0.07)" stroke-width="0.5"/>
    <text x="150" y="18" text-anchor="middle" fill="#585455" font-size="11" font-family="Outfit,sans-serif">Engagement</text>
    <text x="282" y="112" text-anchor="start" fill="#585455" font-size="11" font-family="Outfit,sans-serif">Consistency</text>
    <text x="238" y="270" text-anchor="middle" fill="#585455" font-size="11" font-family="Outfit,sans-serif">Diversity</text>
    <text x="62" y="270" text-anchor="middle" fill="#585455" font-size="11" font-family="Outfit,sans-serif">Authority</text>
    <text x="8" y="112" text-anchor="end" fill="#585455" font-size="11" font-family="Outfit,sans-serif">Viral</text>
    <!-- DATA: Replace P1x,P1y through P5x,P5y with calculated coordinates -->
    <polygon points="P1x,P1y P2x,P2y P3x,P3y P4x,P4y P5x,P5y" fill="rgba(76,38,38,0.1)" stroke="#4c2626" stroke-width="2"/>
    <circle cx="P1x" cy="P1y" r="4" fill="#4c2626"/>
    <circle cx="P2x" cy="P2y" r="4" fill="#4c2626"/>
    <circle cx="P3x" cy="P3y" r="4" fill="#4c2626"/>
    <circle cx="P4x" cy="P4y" r="4" fill="#4c2626"/>
    <circle cx="P5x" cy="P5y" r="4" fill="#4c2626"/>
  </svg>
  <div style="display:flex;justify-content:center;gap:16px;margin-top:16px;flex-wrap:wrap">
    <!-- Replace XX and badge class per score: badge-good (70+), badge-avg (40-69), badge-low (0-39) -->
    <span class="badge badge-good">Engagement: XX</span>
    <span class="badge badge-avg">Consistency: XX</span>
    <span class="badge badge-good">Diversity: XX</span>
    <span class="badge badge-good">Authority: XX</span>
    <span class="badge badge-low">Viral: XX</span>
  </div>
</div>

<!-- SECTION 2: NICHE DISTRIBUTION -->
<div class="card">
  <div class="card-title">Niche Distribution</div>
  <div class="card-subtitle">Based on topic analysis</div>
  <!-- Repeat .bar-row for each niche. Use colors in order: #4c2626, #009588, #104e64, #fcbb00, #f99c00 -->
  <div class="bar-row">
    <div class="bar-label"><span class="bar-name">TOPIC_1</span><span class="bar-pct">XX%</span></div>
    <div class="bar-track"><div class="bar-fill" style="width:XX%;background:#4c2626"></div></div>
  </div>
  <div class="bar-row">
    <div class="bar-label"><span class="bar-name">TOPIC_2</span><span class="bar-pct">XX%</span></div>
    <div class="bar-track"><div class="bar-fill" style="width:XX%;background:#009588"></div></div>
  </div>
  <div class="bar-row">
    <div class="bar-label"><span class="bar-name">TOPIC_3</span><span class="bar-pct">XX%</span></div>
    <div class="bar-track"><div class="bar-fill" style="width:XX%;background:#104e64"></div></div>
  </div>
</div>

<!-- SECTION 3: KEY METRICS -->
<div class="card">
  <div class="card-title">Key Metrics</div>
  <div class="card-subtitle">Profile overview</div>
  <div class="metrics-grid">
    <div class="metric-item"><div class="metric-value">XXX</div><div class="metric-label">Avg. Length</div></div>
    <div class="metric-item"><div class="metric-value">XX%</div><div class="metric-label">Question Ratio</div></div>
    <div class="metric-item"><div class="metric-value">XX%</div><div class="metric-label">Media Ratio</div></div>
    <div class="metric-item"><div class="metric-value">TONE</div><div class="metric-label">Primary Tone</div></div>
    <div class="metric-item"><div class="metric-value">XX%</div><div class="metric-label">CTA Ratio</div></div>
    <div class="metric-item"><div class="metric-value">X.X/day</div><div class="metric-label">Tweet Frequency</div></div>
  </div>
</div>

<!-- SECTION 4: DETAILED DIMENSION BREAKDOWN -->
<div class="card">
  <div class="card-title">Detailed Breakdown</div>
  <div class="card-subtitle">Algorithm-weighted performance across 8 dimensions</div>
  <!-- Repeat .breakdown-row for each dimension. FILL_COLOR: #009588 (7+), #fcbb00 (4-6), #e40014 (0-3) -->
  <!-- FILL_WIDTH = (subscore/10) × 100 + "%" -->
  <div class="breakdown-row">
    <span class="breakdown-label">Content Quality</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Hook Strength</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Consistency & Frequency</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Reply Triggers</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Hashtag Strategy</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Link Strategy</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Media Usage</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Community Engagement (Reply)</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
</div>

<!-- SECTION 5: KEY FINDINGS -->
<div class="card">
  <div class="card-title">Key Findings</div>
  <div class="card-subtitle">What's working and what to improve</div>

  <!-- STRENGTHS: Repeat .finding for each strength -->
  <div class="finding" style="display:flex;gap:12px;padding:14px 0;border-bottom:1px solid rgba(36,33,33,0.06)">
    <div style="flex-shrink:0;width:28px;height:28px;background:rgba(0,149,136,0.12);border-radius:50%;display:flex;align-items:center;justify-content:center">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#009588" stroke-width="3" stroke-linecap="round"><polyline points="20 6 9 17 4 12"/></svg>
    </div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">STRENGTH_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">STRENGTH_DESCRIPTION — explain why this is good and which algorithm rule it leverages.</div>
    </div>
  </div>

  <!-- Repeat more .finding blocks for additional strengths -->

  <!-- WEAKNESSES: Repeat .finding for each area to improve -->
  <div class="finding" style="display:flex;gap:12px;padding:14px 0;border-bottom:1px solid rgba(36,33,33,0.06)">
    <div style="flex-shrink:0;width:28px;height:28px;background:rgba(252,187,0,0.15);border-radius:50%;display:flex;align-items:center;justify-content:center">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#a36100" stroke-width="3" stroke-linecap="round"><line x1="12" y1="2" x2="12" y2="14"/><circle cx="12" cy="19" r="1" fill="#a36100"/></svg>
    </div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">WEAKNESS_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">WEAKNESS_DESCRIPTION — explain what's wrong and what specific action to take, citing the algorithm rule number.</div>
    </div>
  </div>

  <!-- Repeat more .finding blocks for additional weaknesses -->

  <!-- CRITICAL ISSUES (if any): red icon -->
  <div class="finding" style="display:flex;gap:12px;padding:14px 0;">
    <div style="flex-shrink:0;width:28px;height:28px;background:rgba(228,0,20,0.1);border-radius:50%;display:flex;align-items:center;justify-content:center">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#e40014" stroke-width="3" stroke-linecap="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
    </div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">CRITICAL_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">CRITICAL_DESCRIPTION — explain the severe impact and the urgent action needed.</div>
    </div>
  </div>
</div>

<!-- SECTION 6: ALGORITHM-BASED RECOMMENDATIONS -->
<div class="card">
  <div class="card-title">Recommendations</div>
  <div class="card-subtitle">Personalized action items based on the X algorithm</div>

  <!-- Repeat .rec for each recommendation (3-5 items) -->
  <div class="rec" style="display:flex;gap:12px;padding:14px 0;border-bottom:1px solid rgba(36,33,33,0.06)">
    <div style="flex-shrink:0;width:28px;height:28px;background:#4c2626;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:13px;font-weight:700">1</div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">RECOMMENDATION_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">RECOMMENDATION_DETAIL — specific, actionable advice. Reference the relevant algorithm rule (e.g. "Rule 7: replies are 27x more valuable").</div>
      <div style="margin-top:6px"><span class="badge badge-good" style="font-size:10px">Expected impact: HIGH</span></div>
    </div>
  </div>

  <div class="rec" style="display:flex;gap:12px;padding:14px 0;border-bottom:1px solid rgba(36,33,33,0.06)">
    <div style="flex-shrink:0;width:28px;height:28px;background:#4c2626;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:13px;font-weight:700">2</div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">RECOMMENDATION_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">RECOMMENDATION_DETAIL</div>
      <div style="margin-top:6px"><span class="badge badge-avg" style="font-size:10px">Expected impact: MEDIUM</span></div>
    </div>
  </div>

  <div class="rec" style="display:flex;gap:12px;padding:14px 0;">
    <div style="flex-shrink:0;width:28px;height:28px;background:#4c2626;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:13px;font-weight:700">3</div>
    <div>
      <div style="font-size:14px;font-weight:600;color:#242121;margin-bottom:2px">RECOMMENDATION_TITLE</div>
      <div style="font-size:13px;color:#585455;line-height:1.5">RECOMMENDATION_DETAIL</div>
      <div style="margin-top:6px"><span class="badge badge-good" style="font-size:10px">Expected impact: HIGH</span></div>
    </div>
  </div>
</div>

</body>
</html>
```

Coordinate formula: center (150,140), radius 110. Angles: 270°, 342°, 54°, 126°, 198°.
```
x = 150 + (score/100) × 110 × cos(angle_in_radians)
y = 140 + (score/100) × 110 × sin(angle_in_radians)
```

---

## TEMPLATE 2 — Tweet Score (Gauge Meter)

Use after scoring a tweet. Shows gauge + breakdown bars.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:#f5f3f0; font-family:'Outfit',system-ui,sans-serif; color:#242121; padding:20px; }
  .card { background:#fff; border:1px solid rgba(36,33,33,0.15); border-radius:10px; padding:24px; margin-bottom:16px; }
  .card-title { font-family:'Instrument Serif',Georgia,serif; font-style:italic; color:#4c2626; font-size:1.3rem; margin-bottom:4px; }
  .card-subtitle { color:#585455; font-size:13px; margin-bottom:20px; }
  .breakdown-row { display:flex; align-items:center; padding:10px 0; border-bottom:1px solid rgba(36,33,33,0.06); }
  .breakdown-row:last-child { border-bottom:none; }
  .breakdown-label { flex:1; font-size:13px; color:#585455; }
  .breakdown-bar { flex:2; margin:0 12px; background:#edebe7; border-radius:4px; height:6px; overflow:hidden; }
  .breakdown-fill { height:100%; border-radius:4px; }
  .breakdown-score { font-size:13px; font-weight:600; min-width:40px; text-align:right; }
</style>
</head>
<body>

<!-- GAUGE -->
<div class="card" style="text-align:center">
  <div class="card-title">Tweet Score</div>
  <div class="card-subtitle">Algorithm evaluation</div>
  <svg viewBox="0 0 200 130" style="max-width:220px;margin:0 auto;display:block">
    <path d="M 20 110 A 80 80 0 0 1 180 110" fill="none" stroke="#edebe7" stroke-width="14" stroke-linecap="round"/>
    <!-- SCORE_COLOR: #009588 for 70+, #fcbb00 for 40-69, #e40014 for 0-39 -->
    <!-- FILLED = (score/100) × 251 -->
    <path d="M 20 110 A 80 80 0 0 1 180 110" fill="none" stroke="SCORE_COLOR" stroke-width="14" stroke-linecap="round" stroke-dasharray="FILLED 251"/>
    <text x="100" y="100" text-anchor="middle" fill="#242121" font-size="40" font-weight="700" font-family="Outfit,sans-serif">SCORE</text>
    <text x="100" y="120" text-anchor="middle" fill="#585455" font-size="12" font-family="Outfit,sans-serif">/ 100</text>
  </svg>
  <!-- SCORE_LABEL: "Excellent!" / "Good, room to improve" / "Needs work" -->
  <p style="color:#585455;font-size:14px;margin-top:12px">SCORE_LABEL</p>
</div>

<!-- BREAKDOWN -->
<div class="card">
  <div class="card-title">Detailed Breakdown</div>
  <div class="card-subtitle">How your tweet scores across each dimension</div>
  <!-- Repeat for each criterion. FILL_COLOR based on individual score: #009588 / #fcbb00 / #e40014 -->
  <!-- FILL_WIDTH = (subscore/10) × 100 + "%" -->
  <div class="breakdown-row">
    <span class="breakdown-label">Reply Trigger</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Hook Strength</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Link Strategy</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Hashtag Usage</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Media Potential</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Style Match</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">CTA Presence</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
  <div class="breakdown-row">
    <span class="breakdown-label">Standalone Value</span>
    <div class="breakdown-bar"><div class="breakdown-fill" style="width:FILL_WIDTH;background:FILL_COLOR"></div></div>
    <span class="breakdown-score" style="color:FILL_COLOR">X/10</span>
  </div>
</div>

</body>
</html>
```

---

## TEMPLATE 3 — Comparison Table

Use for style comparison between two accounts.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:#f5f3f0; font-family:'Outfit',system-ui,sans-serif; color:#242121; padding:20px; }
  .card { background:#fff; border:1px solid rgba(36,33,33,0.15); border-radius:10px; padding:24px; }
  .card-title { font-family:'Instrument Serif',Georgia,serif; font-style:italic; color:#4c2626; font-size:1.3rem; margin-bottom:16px; }
  table { width:100%; border-collapse:collapse; }
  th { text-align:left; padding:10px 8px; font-size:12px; font-weight:500; color:#585455; text-transform:uppercase; letter-spacing:0.05em; border-bottom:2px solid rgba(36,33,33,0.15); }
  th.u1 { text-align:center; color:#4c2626; }
  th.u2 { text-align:center; color:#009588; }
  td { padding:12px 8px; font-size:14px; border-bottom:1px solid rgba(36,33,33,0.06); }
  td.val { text-align:center; font-weight:500; }
  .winner { font-weight:700; }
</style>
</head>
<body>

<div class="card">
  <div class="card-title">Style Comparison</div>
  <table>
    <thead>
      <tr>
        <th>Metric</th>
        <th class="u1">@USER1</th>
        <th class="u2">@USER2</th>
      </tr>
    </thead>
    <tbody>
      <!-- Repeat rows. Add class="winner" to the higher value cell -->
      <tr><td>Avg. Length</td><td class="val">VAL1</td><td class="val winner">VAL2</td></tr>
      <tr><td>Question Ratio</td><td class="val winner">VAL1</td><td class="val">VAL2</td></tr>
      <tr><td>CTA Ratio</td><td class="val">VAL1</td><td class="val">VAL2</td></tr>
      <tr><td>Media Ratio</td><td class="val">VAL1</td><td class="val">VAL2</td></tr>
      <tr><td>Emoji Usage</td><td class="val">VAL1</td><td class="val">VAL2</td></tr>
      <tr><td>Primary Tone</td><td class="val">VAL1</td><td class="val">VAL2</td></tr>
      <tr><td>Engagement Score</td><td class="val">VAL1</td><td class="val winner">VAL2</td></tr>
    </tbody>
  </table>
</div>

</body>
</html>
```

---

## TEMPLATE 4 — Thread Score Summary

Use after scoring a thread to show per-tweet scores.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:#f5f3f0; font-family:'Outfit',system-ui,sans-serif; color:#242121; padding:20px; }
  .card { background:#fff; border:1px solid rgba(36,33,33,0.15); border-radius:10px; padding:24px; max-width:420px; margin:0 auto; }
  .card-title { font-family:'Instrument Serif',Georgia,serif; font-style:italic; color:#4c2626; font-size:1.3rem; margin-bottom:16px; }
  .tweet-row { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid rgba(36,33,33,0.06); }
  .tweet-row:last-child { border-bottom:none; }
  .tweet-label { font-size:13px; color:#585455; }
  .tweet-score { font-size:15px; font-weight:600; }
  .avg-row { display:flex; justify-content:space-between; align-items:center; padding:14px 0 0; margin-top:8px; border-top:2px solid rgba(36,33,33,0.15); }
  .avg-label { font-size:15px; font-weight:600; color:#242121; }
  .avg-score { font-size:1.4rem; font-weight:700; }
</style>
</head>
<body>

<div class="card">
  <div class="card-title">Thread Score Summary</div>
  <!-- Repeat .tweet-row. SCORE_COLOR: #009588 (70+), #fcbb00 (40-69), #e40014 (0-39) -->
  <div class="tweet-row">
    <span class="tweet-label">Tweet 1 — Hook</span>
    <span class="tweet-score" style="color:SCORE_COLOR">XX/100</span>
  </div>
  <div class="tweet-row">
    <span class="tweet-label">Tweet 2</span>
    <span class="tweet-score" style="color:SCORE_COLOR">XX/100</span>
  </div>
  <div class="tweet-row">
    <span class="tweet-label">Tweet 3</span>
    <span class="tweet-score" style="color:SCORE_COLOR">XX/100</span>
  </div>
  <div class="tweet-row">
    <span class="tweet-label">Tweet 4 — CTA</span>
    <span class="tweet-score" style="color:SCORE_COLOR">XX/100</span>
  </div>
  <div class="avg-row">
    <span class="avg-label">Average</span>
    <span class="avg-score" style="color:SCORE_COLOR">XX/100</span>
  </div>
</div>

</body>
</html>
```
