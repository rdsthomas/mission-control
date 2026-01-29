# Changelog

All notable changes to Mission Control will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-29

### Added
- 🎛️ **Kanban Dashboard** — Five-column board (Permanent, Backlog, In Progress, Review, Done)
- 🤖 **AI Integration** — MoltBot can create, update, and complete tasks via chat
- 👆 **Drag & Drop** — Move tasks between columns visually
- 🔄 **GitHub Sync** — Auto-save tasks to your repository
- 🔔 **Webhook Support** — Real-time notifications when tasks change
- 📁 **Projects & Tags** — Organize tasks by project and context
- 🎨 **Task Editor** — Rich editing with subtasks, comments, and metadata
- 📖 **Onboarding Guide** — Interactive setup wizard for first-time users
- 🔧 **CLI Tools** — `mc-update.sh` for programmatic task management
- 📚 **Architecture Docs** — Detailed technical documentation

### Technical
- Single-file HTML dashboard (no build step required)
- GitHub Pages deployment ready
- Tailscale Funnel compatible for webhooks
- MIT License

---

## Links

- **Demo:** https://rdsthomas.github.io/mission-control/
- **Documentation:** [ARCHITECTURE.md](ARCHITECTURE.md)
- **Issues:** [GitHub Issues](https://github.com/rdsthomas/mission-control/issues)
