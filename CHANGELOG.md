# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2026-03-14

### Added
- Initial release
- 5 slash commands: `/x-advisor`, `/x-tweet`, `/x-score`, `/x-style`, `/x-trends`
- 3 specialized agents: `style-analyst`, `tweet-writer`, `score-evaluator`
- 16 algorithm rules from X's open-source ranking system
- xquik MCP integration with OAuth support (81 endpoints, 100% coverage)
- xquik-branded HTML/SVG artifact templates (analysis report, tweet score, comparison, thread summary)
- User profile persistence via `.claude/x-algorithm-advisor.local.md`
- SessionStart hook for automatic MCP connectivity check
- Freemium-aware 402 handling with graceful degradation
- Design system reference (`design-system.md`) as single source of truth

### Files that need updating when xquik API changes
- `skills/x-algorithm/references/xquik-api.md` — endpoint reference
- `skills/x-algorithm/references/call-rules.md` — if new free/paid categories added
- `commands/*.md` — if new endpoints are used in commands
