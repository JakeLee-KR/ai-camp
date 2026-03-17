# Block 5: Cross-tool Queries + Homework

## EXPLAIN

The real power isn't connecting one tool — it's connecting **multiple tools** and letting Claude work across them.

### What is a Cross-tool Query?

Instead of:
1. Open Slack → find messages → copy
2. Open Google Sheets → paste → format
3. Open Jira → create ticket

You say:
```
"Collect customer complaints from #support this week,
 categorize them in a spreadsheet,
 and create Jira tickets for the top issues"
```

Claude does all 3 automatically.

### Cross-tool Query Examples by Role

**HR:**
```
"Check #hiring on Slack for interview feedback this week,
 summarize by candidate, and create a Google Doc report"
```

**Marketing:**
```
"Pull this week's HubSpot campaign metrics,
 compare with last week's, and post a summary to #marketing"
```

**Sales:**
```
"Look up {client name} in HubSpot, find recent Slack conversations
 about them, and create a meeting prep brief in Google Docs"
```

**Operations:**
```
"Read the vendor proposals from Confluence,
 create a comparison table in Google Sheets,
 and post the recommendation to #procurement"
```

### Tips for Good Cross-tool Queries

| Do | Don't |
|----|-------|
| Name specific channels/folders | Say "check everything" |
| Specify the time range | Leave it open-ended |
| Define the output format | Let Claude guess |
| Name the output location | Forget where to save |

### Your Connected Tools Summary

By now you should have:

| Tool | Method | Status |
|------|--------|--------|
| Slack | Plugin | Connected |
| Jira & Confluence | MCP Server | Connected |
| Google Workspace | CLI Tool (gws) | Connected |
| HubSpot | MCP + OAuth | Optional |

### Managing Your Connections

📱 **Desktop App:** Type `/mcp` to view and manage all your connections, re-authenticate, or remove a connection.

💻 **Terminal** (alternative):
```bash
claude mcp list          # See all your connections
claude mcp remove <name> # Remove a connection
```

---

## Homework — Before Day 3

**Complete these before tomorrow:**

1. **Verify all connections work** — run a simple query for each connected tool
2. **Run 1 cross-tool query** that does something genuinely useful for your work
3. **Write down 3 automation ideas** — tasks you'd like Claude to handle for you

### Why This Matters for Day 3

Tomorrow you'll build your first **Skill** — a reusable custom command. The more tools you have connected, the more powerful your skill can be.

### Automation Ideas Starter List

Think about tasks where you currently:
- **Copy-paste between tools** → Claude can read from one and write to another
- **Follow the same steps every time** → Claude can follow those steps as a skill
- **Compile information from multiple sources** → Claude can gather and summarize

| Pattern | Example |
|---------|---------|
| Collect → Summarize | Slack messages → weekly digest |
| Monitor → Alert | New Jira tickets → Slack notification |
| Request → Generate | "New hire starting" → full onboarding pack |
| Analyze → Report | HubSpot data → formatted report |

## EXECUTE

📱 **Desktop App:**

1. Try a cross-tool query that helps your actual work
2. Create your automation ideas file — type this in your Desktop App:

```
Create a file called automation-ideas.md with 3 task
automation ideas based on the tools I have connected. For each idea:
- The task I do manually today
- Which tools are involved
- What the automated version would look like
- How much time it would save per week
```

This file will be your starting point for Day 3.

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "What's the most important thing to bring to Day 3?",
    "header": "Homework Check",
    "options": [
      {"label": "A list of every tool connection method", "description": ""},
      {"label": "Working tool connections and 3 automation ideas from your real work", "description": ""},
      {"label": "A finished automation project", "description": ""},
      {"label": "Nothing — Day 3 starts fresh", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "Working tool connections and 3 automation ideas from your real work"

If correct: "Perfect! Day 3 is all about building YOUR skill for YOUR work. The connected tools give Claude the reach, and your ideas give it direction. See you tomorrow!"
If incorrect: "Tomorrow you'll build a real automation for your job. To make the most of it, have your tools connected (so Claude can access them) and your ideas ready (so you know what to build). That preparation makes Day 3 productive."
