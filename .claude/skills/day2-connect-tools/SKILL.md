---
name: day2-connect-tools
description: "Internal Camp Day 2: Connect your work tools to Claude Code. Covers Connectors in Claude Desktop App for Slack, Jira, Confluence, Google Workspace, and HubSpot. Use for \"Day 2\", \"connect tools\", \"Slack\", \"Google Drive\", \"Jira\", \"HubSpot\", \"Connectors\"."
---

# Day 2: Connect Your Work Tools

## 🎯 The Goal

> **Claude is connected to your daily work tools.**
>
> By the end of today, Claude will be able to read your Slack, check your calendar, look up Jira tickets, and query HubSpot — all through simple Connectors in the Desktop App. You'll run your first cross-tool query.

---

## STOP PROTOCOL

> Same 2-turn protocol as Day 1. Never violate.

### Each block = 2 turns

```
Phase A: Print BLOCK BANNER → Explain + Execute instructions → STOP (no questions)
Phase B: Quiz + feedback → next block
```

### Block Banner

At the **very start** of every Phase A, print this banner so the user can easily find where the new block begins:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📘 BLOCK {N}: {BLOCK TITLE}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Phase A must end with:
```
---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.
```

---

## Block Map

| Block | File | Topic |
|-------|------|-------|
| 0 | `references/block0-why-connect-tools.md` | Why connect tools + Connectors overview |
| 1 | `references/block1-install-claude-code.md` | Enable Claude Code in Claude Desktop App |
| 2 | `references/block2-connect-slack.md` | Connect Slack via Connectors |
| 3 | `references/block3-connect-jira-confluence.md` | Connect Jira & Confluence via Connectors |
| 4 | `references/block4-connect-google-workspace.md` | Connect Google Workspace via Connectors |
| 5 | `references/block5-connect-hubspot.md` | Connect HubSpot via Connectors (Optional) |
| 6 | `references/block6-cross-tool-and-homework.md` | Cross-tool queries + Homework |

---

## Interaction Rules

- One block at a time
- Before Block 2, briefly check which tools the participant uses (Slack, Google Workspace, Jira, Confluence, HubSpot)
- Walk through each step carefully — these are non-engineers
- All tool connections use **Settings → Connectors → Browse Connectors** in the Desktop App
- If something fails, troubleshoot patiently before moving on
- Language: English
- Tone: patient, encouraging — tool setup can be frustrating

---

## Start

```
AskUserQuestion({
  "questions": [{
    "question": "Where would you like to start?",
    "header": "Day 2: Connect Tools",
    "options": [
      {"label": "Block 0: Why Connect Tools?", "description": "Overview of how Claude connects to external tools"},
      {"label": "Block 1: Enable Claude Code", "description": "Enable Claude Code inside Claude Desktop App"},
      {"label": "Block 2: Connect Slack", "description": "Connect Slack via Settings → Connectors"},
      {"label": "Block 3: Connect Jira & Confluence", "description": "Connect Atlassian tools via Connectors"},
      {"label": "Block 4: Google Workspace", "description": "Connect Google Calendar, Drive, Docs, Gmail"},
      {"label": "Block 5: Connect HubSpot (Optional)", "description": "Connect HubSpot CRM via Connectors"}
    ],
    "multiSelect": false
  }]
})
```
