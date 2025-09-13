# 🌟 DevMind v2.0 — The AI-Powered Developer Co-Pilot (Trello Edition)

> Every GitHub push → Auto-creates an AI-summarized Trello card → Notifies team on Telegram → Lets team approve/reject with buttons → Logs metrics → Sends weekly digest — all without manual work.

![DevMind Workflow Diagram](screenshots/n8n-workflow.png)

---

## 💡 What Is DevMind?

**DevMind** is an intelligent automation system that turns code pushes into structured, trackable, and collaborative actions — transforming chaotic commits into organized, team-aligned development workflows.

It’s not just a bot.  
It’s your **AI-powered co-pilot for DevOps**.

---

## 🔧 Tech Stack

| Tool                          | Purpose                                                                   |
| ----------------------------- | ------------------------------------------------------------------------- |
| **n8n**                       | Workflow automation engine                                                |
| **GitHub**                    | Trigger: listens for `push` events                                        |
| **Trello**                    | AI-powered task management (Atlassian Intelligence auto-summarizes cards) |
| **Telegram**                  | Real-time alerts + interactive buttons (✅ Approve / ❌ Reject)           |
| **OpenAI**                    | Detects risky commits (e.g., `rm -rf`, secrets)                           |
| **Google Sheets**             | Logs all activity for analytics and audit trails                          |
| **GitHub Actions (optional)** | Auto-backup workflow `.json` to Gist                                      |

---

## 🚀 Features

| Feature                            | Description                                                            |
| ---------------------------------- | ---------------------------------------------------------------------- |
| ✅ **Smart Branch Guardrails**     | Blocks direct pushes to `main` unless via PR                           |
| ✅ **AI-Powered Card Creation**    | Trello auto-summarizes commit context using Atlassian Intelligence     |
| ✅ **Risk Detection**              | OpenAI flags dangerous commits (`CRITICAL`, `HIGH`)                    |
| ✅ **Interactive Telegram Alerts** | Team clicks “✅ Approve” or “❌ Reject” → card moves in Trello         |
| ✅ **Auto-Logging**                | All commits logged to Google Sheets with timestamp, author, risk level |
| ✅ **Admin Alerts**                | Instant Telegram alert if `CRITICAL` risk detected                     |
| ✅ **Weekly Digest**               | Every Monday, AI sends a summary of last week’s activity               |
| ✅ **Auto-Backup**                 | Workflow exported to private GitHub Gist on every run                  |

---

## 📸 Screenshots

| Screenshot                                            | Description                              |
| ----------------------------------------------------- | ---------------------------------------- |
| ![Workflow Graph](screenshots/n8n-workflow.png)       | Full n8n automation flow                 |
| ![Trello Card](screenshots/trello-card.png)           | AI-generated card with commit context    |
| ![Telegram Message](screenshots/telegram-message.png) | Rich message with approve/reject buttons |
| ![Weekly Digest](screenshots/weekly-digest.png)       | AI-written weekly dev summary            |
| ![Google Sheets Log](screenshots/sheets-log.png)      | Live audit trail of all activity         |

> _Screenshots are included in the `/screenshots` folder._

---

## 🔐 Setup Guide

### 1. Prerequisites

- [n8n.cloud](https://n8n.io/cloud/) (free tier)
- GitHub account + repo
- Trello account (Free plan works)
- Telegram bot (@BotFather) + chat ID
- OpenAI API key ([platform.openai.com](https://platform.openai.com))
- Google Sheet (for logging)

### 2. Get Your Keys

| Key                                       | Where to Find                                                                  |
| ----------------------------------------- | ------------------------------------------------------------------------------ |
| `GITHUB_TOKEN`                            | GitHub → Settings → Developer Settings → Personal Access Tokens (`repo` scope) |
| `TELEGRAM_BOT_TOKEN`                      | Talk to @BotFather on Telegram                                                 |
| `TELEGRAM_CHAT_ID`                        | Use @userinfobot on Telegram                                                   |
| `TRELLO_API_KEY` & `TRELLO_TOKEN`         | [trello.com/app-key](https://trello.com/app-key)                               |
| `TRELLO_BOARD_ID` & `TRELLO_LIST_TODO_ID` | Enable Developer Mode in Trello → hover list → copy ID                         |
| `OPENAI_API_KEY`                          | [platform.openai.com/api-keys](https://platform.openai.com/api-keys)           |
| `GOOGLE_SHEET_ID`                         | From Google Sheet URL: `d/1aBcDeFgHiJkLmNoPqRsTuVwXyZ/edit`                    |

### 3. Configure Webhook

1. Copy your n8n webhook URL from the **Webhook node**
2. Go to GitHub → Settings → Webhooks → Add Webhook
   - Payload URL: `https://your-n8n-instance.com/webhook/...`
   - Content type: `application/json`
   - Secret: `my-devmind-secret-xyz` _(create one)_
   - Events: ✅ Only `push`
   - Active: ✔️

### 4. Import Workflow

1. Download [`devmind.json`](workflow/devmind.json)
2. In n8n → Click “Import” → Upload file
3. Replace all placeholder keys with your own
4. Click “Save” → “Activate”

### 5. Test It!

Push a commit:

```bash
echo "# test" >> README.md
git add README.md
git commit -m "test: trigger DevMind"
git push origin main
```
