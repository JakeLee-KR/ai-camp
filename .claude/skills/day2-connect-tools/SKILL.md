---
name: day2-connect-tools
description: "Internal Camp Day 2: Connect your work tools to Claude Code. Covers plugins, MCP servers, CLI tools, and step-by-step guides for Slack, Jira, Confluence, Google Workspace, and HubSpot. Use for \"Day 2\", \"connect tools\", \"Slack\", \"Google Drive\", \"Jira\", \"HubSpot\", \"MCP\"."
---

# Day 2: Connect Your Work Tools

This skill teaches participants to connect their daily work tools (Slack, Jira, Confluence, Google Workspace, HubSpot) to Claude Code using various methods — plugins, MCP servers, and CLI tools — then run cross-tool queries.

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
| 0 | `references/block0-why-connect-tools.md` | Why connect tools + connection methods overview |
| 1 | `references/block1-install-claude-code.md` | Install Claude Code in Claude Desktop App |
| 2 | `references/block2-connect-slack.md` | Step 1: Connect Slack |
| 3 | `references/block3-connect-jira-confluence.md` | Step 2: Connect Jira & Confluence |
| 4 | `references/block4-connect-google-workspace.md` | Step 3: Connect Google Workspace |
| 5 | `references/block5-connect-hubspot.md` | Step 4: Connect HubSpot (Optional) |
| 6 | `references/block6-cross-tool-and-homework.md` | Cross-tool queries + Homework |

---

## Interaction Rules

- One block at a time
- Before Block 1, briefly check which tools the participant uses (Slack, Google Workspace, Jira, Confluence, HubSpot)
- Walk through each step carefully — these are non-engineers
- Each block has step-by-step instructions for Claude Desktop App (and Terminal when needed)
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
      {"label": "Block 1: Install Claude Code", "description": "Install Claude Code inside Claude Desktop App"},
      {"label": "Block 2: Connect Slack", "description": "Install Slack plugin and test it"},
      {"label": "Block 3: Connect Jira & Confluence", "description": "Connect Atlassian tools via MCP"},
      {"label": "Block 4: Google Workspace", "description": "Connect Google Calendar, Drive, Docs, and more"},
      {"label": "Block 5: Connect HubSpot (Optional)", "description": "Connect HubSpot CRM via MCP"}
    ],
    "multiSelect": false
  }]
})
```
