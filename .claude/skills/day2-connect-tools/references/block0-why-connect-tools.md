# Block 0: Why Connect Tools?

## EXPLAIN

By default, Claude Code can only work with **files on your computer**. But your real work lives in Slack, Jira, Google Calendar, HubSpot, and more. Today we'll give Claude access to those tools.

### The Before & After

```
Before connecting tools:
  You ←→ Claude Code ←→ Files on your computer

After connecting tools:
  You ←→ Claude Code ←→ Slack
                      ←→ Jira & Confluence
                      ←→ Google Calendar, Drive, Docs
                      ←→ HubSpot
                      ←→ (and more)
```

### Real Examples

| What you say | What Claude does |
|--------------|------------------|
| "What's happening in #swingvy_general?" | Reads your Slack channel and summarizes |
| "What are my open Jira issues?" | Fetches your assigned Jira issues |
| "What's my upcoming schedule?" | Checks your Google Calendar |
| "Show me recent HubSpot contacts" | Queries your CRM |

### How Do Connections Work?

Claude Code connects to external tools in several ways:

| Method | What it is | Example |
|--------|-----------|---------|
| **Plugin** | One-command install, easiest | `claude plugin install slack` |
| **MCP Server** | A connector that translates between Claude and a tool | `claude mcp add atlassian ...` |
| **CLI Tool + Skill** | A command-line tool that Claude calls directly | Google Workspace (`gws`) |

You don't need to understand the technical details — just follow the steps for each tool.

### Today's Plan

We'll connect **4 tools** step by step:

| Step | Tool | Method | Difficulty |
|------|------|--------|------------|
| 1 | Slack | Plugin | Easy |
| 2 | Jira & Confluence | MCP Server | Easy |
| 3 | Google Workspace | CLI Tool | Medium |
| 4 | HubSpot (Optional) | MCP + OAuth | Medium |

## EXECUTE

Let's see what connections you already have (probably none yet, and that's fine).

In **Claude Desktop App**, type `/mcp` and press Enter. This shows your current connections.

If nothing appears, that's expected! We'll connect your first tool in the next block.

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "What does connecting tools do for Claude Code?",
    "header": "Concept Quiz",
    "options": [
      {"label": "Makes Claude Code faster", "description": ""},
      {"label": "Lets Claude access external tools like Slack, Jira, and Google Calendar", "description": ""},
      {"label": "Adds a graphical interface to Claude Code", "description": ""},
      {"label": "Replaces your work tools with Claude", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "Lets Claude access external tools like Slack, Jira, and Google Calendar"

If correct: "Exactly! Connecting tools gives Claude arms that can reach into Slack, Jira, Google Calendar, and more. Without connections, Claude only sees your local files. With them, Claude becomes your work assistant across all your tools."
If incorrect: "Connecting tools lets Claude access your external work tools — Slack, Jira, Google Calendar, HubSpot, etc. Think of each connection as a bridge between Claude and one of your tools. Claude doesn't replace them — it connects to them."
