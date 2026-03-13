# xquik Design System

Single source of truth for all visual artifacts. Referenced by all templates in `templates/`.

## Colors

| Token | Hex | Usage |
|-------|-----|-------|
| Background | `#f5f3f0` | Page background |
| Card | `#ffffff` | Card surfaces |
| Text | `#242121` | Primary text |
| Muted text | `#585455` | Labels, secondary text |
| Border | `rgba(36,33,33,0.15)` | Card borders |
| Accent | `#4c2626` | Brand burgundy, headings, chart-1 |
| Teal | `#009588` | Chart-2, good scores (70+) |
| Dark teal | `#104e64` | Chart-3 |
| Gold | `#fcbb00` | Chart-4, average scores (40-69) |
| Orange | `#f99c00` | Chart-5 |
| Red | `#e40014` | Destructive, low scores (0-39) |
| Muted surface | `#edebe7` | Input backgrounds, track bars |

## Typography

| Element | Font | Weight |
|---------|------|--------|
| Display headings | `'Instrument Serif', Georgia, serif` (italic) | 400 |
| Body text | `'Outfit', system-ui, -apple-system, sans-serif` | 400-700 |
| Monospace | `'JetBrains Mono', monospace` | 400 |

Google Fonts import:
```
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
```

## Layout

| Property | Value |
|----------|-------|
| Border radius | `10px` |
| Card padding | `24px` |
| Max width | `500px` |
| Spacing unit | `4px` |

## Score Thresholds

| Range | Color | Badge class | Label |
|-------|-------|-------------|-------|
| 70-100 | `#009588` (teal) | `badge-good` | Excellent |
| 40-69 | `#fcbb00` (gold) | `badge-avg` | Average |
| 0-39 | `#e40014` (red) | `badge-low` | Low |

For breakdown bars (X/10): 7+ = good, 4-6 = avg, 0-3 = low.

## Radar Chart Geometry

- Center: `(150, 140)`
- Radius: `110`
- 5 axes at angles: 270°, 342°, 54°, 126°, 198°

Coordinate formula:
```
x = 150 + (score/100) × 110 × cos(angle_in_radians)
y = 140 + (score/100) × 110 × sin(angle_in_radians)
```

## Gauge Meter Geometry

- Arc path: `M 20 110 A 80 80 0 0 1 180 110`
- Total arc length: `251` units
- Filled portion: `(score/100) × 251`

## Chart Color Sequence

For multi-series data, cycle: `#4c2626` → `#009588` → `#104e64` → `#fcbb00` → `#f99c00`

## Shared CSS Base

All templates start with this:
```css
@import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@1&family=Outfit:wght@400;500;600;700&display=swap');
* { margin:0; padding:0; box-sizing:border-box; }
body { background:#f5f3f0; font-family:'Outfit',system-ui,-apple-system,sans-serif; color:#242121; padding:20px; }
.card { background:#fff; border:1px solid rgba(36,33,33,0.15); border-radius:10px; padding:24px; margin-bottom:16px; }
.card-title { font-family:'Instrument Serif',Georgia,serif; font-style:italic; color:#4c2626; font-size:1.3rem; margin-bottom:4px; }
.card-subtitle { color:#585455; font-size:13px; margin-bottom:20px; }
.badge { display:inline-block; padding:3px 10px; border-radius:20px; font-size:11px; font-weight:600; }
.badge-good { background:rgba(0,149,136,0.12); color:#009588; }
.badge-avg { background:rgba(252,187,0,0.15); color:#a36100; }
.badge-low { background:rgba(228,0,20,0.1); color:#e40014; }
```
