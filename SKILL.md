---
name: mission-control
description: Kanban-style task management dashboard for AI assistants. Manage tasks via CLI or dashboard UI. Use when user mentions tasks, kanban, task board, mission control, or wants to track work items with status columns (backlog, in progress, review, done).
homepage: https://github.com/rdsthomas/mission-control
metadata: {"clawdbot": {"emoji": "🎛️"}}
---

# Mission Control — Task Management for AI Assistants

A Kanban-style task board that you (the AI assistant) can manage via CLI scripts or direct JSON editing. Includes a web dashboard for the human to visualize and interact with tasks.

## Setup

### First-Time Installation

Run the setup script to copy dashboard files to your workspace:

```bash
# If installed via ClawdHub:
<skill>/scripts/mc-setup.sh <workspace>

# If cloned manually:
./scripts/mc-setup.sh <workspace>
```

This copies from `assets/` to your workspace:
- `index.html` — Dashboard UI
- `data/tasks.json` — Task data (with onboarding guides)
- `scripts/mc-update.sh` — CLI tool
- `.github/workflows/deploy.yml` — GitHub Pages deployment

### Enable GitHub Pages

1. Push your workspace to GitHub
2. Go to Settings → Pages
3. Source: Deploy from branch → main
4. Your dashboard: `https://[username].github.io/[repo]/`

### Webhook Setup (MoltBot Integration)

GitHub sends a webhook directly to MoltBot whenever the repository is pushed (including task changes).

#### Step 1: Set Up Tailscale Funnel

Tailscale creates a secure tunnel so GitHub can reach your local MoltBot:

```bash
# Install Tailscale
brew install tailscale  # macOS
# or: curl -fsSL https://tailscale.com/install.sh | sh  # Linux

# Start Tailscale
tailscale up

# Enable Funnel for MoltBot port
tailscale funnel 18789

# Get your URL
tailscale funnel status
# Output: https://your-machine.tail1234.ts.net -> http://127.0.0.1:18789
```

#### Step 2: Add GitHub Webhook

1. Go to your repo → Settings → Webhooks → Add webhook
2. **Payload URL:** `https://your-machine.tail1234.ts.net/hooks/github?token=YOUR_TOKEN`
3. **Content type:** `application/json`
4. **Events:** Select "Just the push event"
5. Click "Add webhook"

Generate a secure token:
```bash
openssl rand -hex 32
```

#### Step 3: Verify

Push a change and check:
- GitHub webhook shows green checkmark (recent deliveries)
- MoltBot receives the notification

---

## Task Structure

Tasks are stored in `<workspace>/data/tasks.json`:

```json
{
  "tasks": [
    {
      "id": "task_001",
      "title": "Implement feature X",
      "description": "Detailed description with context",
      "status": "backlog",
      "project": "devops",
      "tags": ["devops", "feature"],
      "subtasks": [
        { "id": "sub_001", "title": "Research approach", "done": false },
        { "id": "sub_002", "title": "Write code", "done": false }
      ],
      "priority": "high",
      "comments": [],
      "createdAt": "2026-01-28T10:00:00Z"
    }
  ],
  "projects": [
    { "id": "devops", "name": "DevOps", "color": "#3b82f6", "icon": "💻" }
  ],
  "activities": [],
  "lastUpdated": "2026-01-28T10:00:00Z"
}
```

### Status Values

| Status | Column | Meaning |
|--------|--------|---------|
| `permanent` | 🔄 Permanent | Recurring tasks (daily/weekly checks) |
| `backlog` | 📋 Backlog | Waiting to be started |
| `in_progress` | 🚀 In Progress | Currently being worked on |
| `review` | 👀 Review | Done, awaiting human approval |
| `done` | ✅ Done | Completed |

### Priority Values

- `high` — Urgent, do first
- `medium` — Normal priority
- `low` — Can wait

---

## CLI Commands

Use `<skill>/scripts/mc-update.sh` for task management:

```bash
# Change task status
mc-update.sh status <task_id> <new_status>

# Example: Start working on a task
mc-update.sh status task_001 in_progress

# Add a comment
mc-update.sh comment <task_id> "Your comment here"

# Add a subtask
mc-update.sh subtask <task_id> "Subtask title"

# Mark subtask as done
mc-update.sh done <task_id> <subtask_id>

# Complete task (moves to review + adds summary comment)
mc-update.sh complete <task_id> "Completion summary"

# Mark task as being processed (prevents duplicate work)
mc-update.sh start <task_id>

# Push changes to GitHub
mc-update.sh push "Commit message"
```

---

## Workflow

### When Human Creates a Task

Human adds task via dashboard → appears in Backlog.

### When Human Moves Task to "In Progress"

This is your signal to start working! GitHub webhook notifies you.

1. **Read the task** — Check title, description, subtasks
2. **Mark as started** — `mc-update.sh start <task_id>` (prevents duplicate processing)
3. **Work through subtasks** — Mark each done as you complete them
4. **Add progress comments** — Keep human informed
5. **Complete the task** — `mc-update.sh complete <task_id> "Summary of what was done"`

### When Task is in "Review"

Human reviews your work. They may:
- **Approve** → Move to Done
- **Request changes** → Add comment with feedback, move back to In Progress

If moved back to In Progress with a comment, that's feedback for you to address.

### Handling Feedback

When you see a task in "In Progress" with recent comments:
1. Read the feedback comment
2. Address the issues
3. Add a comment explaining your changes
4. Move back to Review

---

## Best Practices

### Writing Good Task Descriptions

Help yourself succeed — write clear descriptions:

```
BAD:  "Fix the bug"
GOOD: "Fix login redirect bug — users redirected to /home instead of /dashboard after OAuth. Check auth callback handler."
```

### Using Subtasks

Break complex tasks into steps:

```json
"subtasks": [
  { "id": "sub_001", "title": "Reproduce the issue", "done": false },
  { "id": "sub_002", "title": "Identify root cause", "done": false },
  { "id": "sub_003", "title": "Implement fix", "done": false },
  { "id": "sub_004", "title": "Write test", "done": false }
]
```

### Adding Useful Comments

Comments create a work log:

```bash
mc-update.sh comment task_001 "Found the bug — redirect URL was hardcoded. Fixing now."
mc-update.sh comment task_001 "Fix deployed. Tested with 3 OAuth providers."
```

### Completion Summaries

When completing, summarize what was done:

```bash
mc-update.sh complete task_001 "Fixed OAuth redirect by using dynamic returnUrl from session. Added regression test. Tested with Google, GitHub, and Microsoft OAuth."
```

---

## Direct JSON Editing

For complex operations, edit `<workspace>/data/tasks.json` directly:

### Add a New Task

```python
import json
from datetime import datetime

with open('data/tasks.json', 'r') as f:
    data = json.load(f)

new_task = {
    "id": f"task_{len(data['tasks']) + 1:03d}",
    "title": "New task title",
    "description": "Task description",
    "status": "backlog",
    "project": "devops",
    "tags": ["devops"],
    "subtasks": [],
    "priority": "medium",
    "comments": [],
    "createdAt": datetime.utcnow().isoformat() + "Z"
}

data['tasks'].append(new_task)
data['lastUpdated'] = datetime.utcnow().isoformat() + "Z"

with open('data/tasks.json', 'w') as f:
    json.dump(data, f, indent=2)
```

---

## Integration with Heartbeat

Add to your `<workspace>/HEARTBEAT.md`:

```markdown
## Task Check

1. Check `data/tasks.json` for tasks with status "in_progress"
2. If any have `processingStartedAt` but no recent activity, flag as potentially stale
3. Check for tasks in "review" with new comments (feedback to address)
```

---

## Troubleshooting

### Dashboard shows sample data

You're not logged in. Click "Connect GitHub" and add your Personal Access Token with `repo` scope.

### Changes not appearing

GitHub Pages caches content. Try:
- Hard refresh (Cmd+Shift+R)
- Wait 1-2 minutes for deploy
- Check Actions tab for deploy status

### Webhook not triggering

1. Check repo Settings → Webhooks → Recent Deliveries
2. Verify Tailscale Funnel is running: `tailscale funnel status`
3. Check MoltBot logs for incoming webhook

---

## Files Reference

| File | Purpose |
|------|---------|
| `<workspace>/index.html` | Dashboard UI |
| `<workspace>/data/tasks.json` | Task data |
| `<workspace>/.github/workflows/deploy.yml` | GitHub Pages deployment |
| `<skill>/scripts/mc-update.sh` | CLI tool |
| `<skill>/scripts/mc-setup.sh` | Setup script |
