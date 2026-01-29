# Mission Control 🎛️

**The visual layer your AI assistant is missing.**

> Chat conversations are linear. Projects aren't.

[![Status](https://img.shields.io/badge/status-beta-yellow)](https://github.com/rdsthomas/mission-control)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![MoltBot](https://img.shields.io/badge/MoltBot-compatible-10b981)](https://github.com/moltbot/moltbot)
[![Discord](https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2)](https://discord.gg/clawd)

![Mission Control Dashboard](docs/images/dashboard.png)

---

## Why Mission Control?

You've set up MoltBot. It's brilliant — answers on WhatsApp, automates your workflows, even writes code for you. But after a week of conversations, you have **50+ tasks scattered across hundreds of messages**.

Where was that API refactor task? Did the dark mode feature get completed? What's actually in progress right now?

**Mission Control gives your AI assistant a visual brain.**

| Without Mission Control | With Mission Control |
|------------------------|---------------------|
| Tasks buried in chat history | All tasks on one Kanban board |
| "What was I working on?" | Instant visual status |
| Lost context between sessions | Persistent, organized backlog |
| AI works, you lose track | AI works, dashboard updates |

---

## Who Is This For?

### 🛠️ Solo Developers & Indie Hackers
You're building products while juggling a dozen parallel workstreams. MoltBot helps you code, but you need to **see** the big picture. Mission Control turns your AI conversations into a project board.

### ⚡ Productivity Enthusiasts
You've optimized everything — but your AI assistant's output is still trapped in linear chat. Mission Control extracts actionable tasks from conversations and tracks them visually.

### 🔒 Self-Hosters & Privacy-Conscious Users
Your data stays yours. Mission Control runs on GitHub Pages from your own repo. No external services, no tracking, no cloud lock-in.

---

## Features

- 📋 **Kanban Board** — Permanent, Backlog, In Progress, Review, Done
- 🤖 **AI-Native** — MoltBot can create, update, and complete tasks via chat
- 👤 **Human-Friendly** — You can drag & drop in the dashboard
- 🔄 **GitHub Sync** — Auto-save to your repo, hosted on GitHub Pages
- 🔔 **Webhooks** — MoltBot gets notified instantly when you move tasks
- 🎨 **Projects & Tags** — Organize by project, filter by context

![Task Editor](docs/images/task-edit.png)

---

## Quick Start

```bash
# Install the skill
clawdhub install mission-control

# Run setup (copies dashboard to your workspace)
./skills/mission-control/scripts/mc-setup.sh ~/your-workspace

# Push to GitHub and enable Pages
cd ~/your-workspace
git add -A && git commit -m "Add Mission Control" && git push
# Then: Settings → Pages → Branch: main
```

**First time?** The dashboard includes an interactive **Onboarding Guide** that walks you through GitHub Pages, webhooks, and Tailscale setup.

---

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                        YOUR WORKFLOW                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  💬 CHAT                           📊 DASHBOARD                 │
│  ─────                             ─────────                    │
│                                                                 │
│  "Plan the Q1 roadmap"      ──►    📋 Backlog: Q1 Roadmap      │
│                                         ├── Feature A           │
│                                         └── Feature B           │
│                                                                 │
│  "Start Feature A"          ──►    🚀 In Progress: Feature A   │
│                                                                 │
│  [MoltBot works...]         ◄──    Updates subtasks & comments │
│                                                                 │
│  [You review in dashboard]  ──►    ✅ Done: Feature A          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Bidirectional:** Both you AND MoltBot can create, edit, move, and complete tasks. Work from the dashboard or via chat — everything stays in sync.

![Settings & Projects](docs/images/settings.png)

---

## Bidirectional Workflow

### Two Ways to Work

| Action | 👤 You (Dashboard) | 🤖 MoltBot (Chat/CLI) |
|--------|-------------------|----------------------|
| Create task | Click "+" button | Natural language or CLI |
| Edit task | Click card → Edit | `mc-update.sh` or JSON |
| Move task | Drag & drop | Change status via CLI |
| Add comment | Type in comment box | `mc-update.sh comment` |
| Complete | Drag to Done | `mc-update.sh complete` |

### Example: Planning via Chat

**You:** *"Let's implement dark mode"*

**MoltBot:** *"I'll create an implementation plan:"*

```
📋 Task: Implement Dark Mode
├── Define color variables (CSS custom properties)
├── Create theme toggle component  
├── Persist preference in localStorage
├── Detect system preference
└── Test across browsers
```

*"Added to your Backlog. Move to In Progress when ready!"*

### Chat Commands

Talk naturally — MoltBot understands:

- *"Create a task for refactoring the auth module"*
- *"Add a subtask: write unit tests"*
- *"Move dark mode to review"*
- *"What's in progress?"*
- *"Archive completed tasks"*

---

## Installation

### Via ClawdHub (Recommended)

```bash
clawdhub install mission-control
./skills/mission-control/scripts/mc-setup.sh ~/your-workspace
```

### Manual

```bash
git clone https://github.com/rdsthomas/mission-control.git
cd mission-control
./scripts/mc-setup.sh ~/your-workspace
```

### Setup Checklist

1. ✅ Enable GitHub Pages (Settings → Pages → Branch: main)
2. ✅ Create GitHub Token ([github.com/settings/tokens](https://github.com/settings/tokens) → repo scope)
3. ✅ Connect Dashboard (paste token in dashboard)
4. ✅ Set up [Tailscale Funnel](https://tailscale.com/kb/1223/funnel) for webhooks
5. ✅ Add GitHub Webhook (Settings → Webhooks)

See [ARCHITECTURE.md](ARCHITECTURE.md) for detailed setup and communication flow.

---

## File Structure

```
mission-control/                  # MoltBot Skill
├── SKILL.md                      # Skill documentation
├── scripts/mc-setup.sh           # Setup script
├── assets/                       # Dashboard files
│   ├── index.html                # Dashboard UI
│   ├── data/tasks.json           # Task data
│   └── scripts/mc-update.sh      # CLI tool
├── docs/images/                  # Screenshots
├── ARCHITECTURE.md               # Technical details
└── README.md                     # This file
```

---

## Troubleshooting

### "Cannot find package 'undici'" during installation

This error comes from the ClawdHub CLI, not Mission Control:

```
Error [ERR_MODULE_NOT_FOUND]: Cannot find package 'undici' imported from .../clawdhub/dist/http.js
```

**Fix:** Reinstall ClawdHub to ensure all dependencies are properly installed:

```bash
npm install -g clawdhub
```

Then retry the installation:

```bash
clawdhub install mission-control
```

---

## Community & Support

- 💬 **Discord:** [discord.gg/clawd](https://discord.gg/clawd) — MoltBot community (8.9K+ members)
- 📖 **Docs:** [ARCHITECTURE.md](ARCHITECTURE.md) — How it all works
- 🐛 **Issues:** [GitHub Issues](https://github.com/rdsthomas/mission-control/issues)
- 🌟 **Star this repo** if Mission Control helps you stay organized!

---

## License

MIT License — see [LICENSE](LICENSE).

Built for [MoltBot](https://github.com/moltbot/moltbot) 🦞

---

<p align="center">
  <b>Stop losing tasks in chat. Start shipping.</b><br>
  <a href="https://rdsthomas.github.io/mission-control/">Try the Demo</a> · <a href="https://discord.gg/clawd">Join Discord</a> · <a href="https://github.com/rdsthomas/mission-control">⭐ Star on GitHub</a>
</p>
