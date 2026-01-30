# Changelog

All notable changes to Mission Control will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-01-30

### ⚠️ Breaking Changes

- **Config Location Changed** — Config now lives in `~/.clawdbot/mission-control.json` instead of being hardcoded
- **Transform Module Renamed** — Now uses `github-mission-control.mjs` (copy to `~/.clawdbot/hooks-transforms/`)
- **Setup Script Removed** — `scripts/mc-setup.sh` is deprecated; use agent-guided setup instead

### Added

- **Dynamic Configuration** — All settings loaded from `~/.clawdbot/mission-control.json`
- **Environment Variable Fallbacks** — Override config via `CLAWDBOT_GATEWAY`, `MC_WORKSPACE`, etc.
- **Agent-Guided Setup** — Say "Set up Mission Control" and the agent handles everything
- **EPIC Support** — Parent tasks can contain child tickets for sequential execution
- **Extended Timeouts for EPICs** — Automatically calculated based on number of children
- **Repo Info from Payload** — No more hardcoded GitHub URLs; extracted from webhook
- **New Documentation**:
  - `docs/PREREQUISITES.md` — Installation requirements
  - `docs/HOW-IT-WORKS.md` — Technical architecture
  - `docs/TROUBLESHOOTING.md` — 10 common issues with solutions
- **Example Configurations**:
  - `assets/examples/mission-control.json`
  - `assets/examples/CONFIG-REFERENCE.md`
  - `assets/examples/clawdbot-hooks-config.json`
  - `assets/examples/HOOKS-CONFIG.md`

### Changed

- **SKILL.md Rewritten** — Focus on agent-guided setup, removed manual steps
- **README.md Simplified** — Quick start section, badges, links to docs
- **Transform Location** — Moved to `assets/transforms/` for distribution

### Removed

- `scripts/mc-setup.sh` — Replaced by agent-guided setup
- Hardcoded paths, tokens, and URLs in transform module
- Manual webhook setup instructions (agent handles this now)

### Fixed

- GitHub API caching issues resolved via Git Blob API
- Snapshot desync on concurrent updates
- HMAC timing attacks prevented with `timingSafeEqual`

## [1.0.0] - 2026-01-28

Initial release.

### Added

- Kanban dashboard (single-page HTML app)
- GitHub Pages deployment
- `mc-update.sh` CLI tool
- Webhook integration with Clawdbot
- Diff-based change detection
- Auto-processing for "In Progress" tasks
- Subtask management
- Comment system
- Activity feed
- Search functionality
- Archive feature for completed tasks
