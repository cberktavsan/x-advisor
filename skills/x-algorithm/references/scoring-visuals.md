# Scoring and Visualization

## Rules

1. NEVER write HTML/SVG visuals as inline text — create an **artifact** for each visual.
2. Use EXACT templates — only replace UPPERCASE placeholders (e.g. `USERNAME`, `SCORE`, `TOPIC`).
3. Colors, fonts, and layout tokens are defined in `design-system.md`.

## Templates

| Template | When to use | File |
|----------|-------------|------|
| Analysis Report | After style analysis (STEP 4) — radar chart, niche bars, metrics, findings, recommendations | `templates/analysis-report.html` |
| Tweet Score | After scoring a single tweet — gauge meter + dimension breakdown | `templates/tweet-score.html` |
| Comparison Table | Style comparison between two accounts | `templates/comparison-table.html` |
| Thread Summary | After scoring a thread — per-tweet scores + average | `templates/thread-summary.html` |
