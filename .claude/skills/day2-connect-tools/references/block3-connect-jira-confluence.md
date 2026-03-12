# Block 2: Connect Jira & Confluence

## EXPLAIN

Now let's connect **Jira and Confluence** — both are Atlassian products, so we connect them together through a single MCP server.

### Step-by-Step Guide

#### Step 1: Add the Atlassian MCP server

In your **Terminal** (outside Claude Code), run:

```bash
claude mcp add --transport http atlassian https://mcp.atlassian.com/v1/mcp
```

This tells Claude Code to connect to Atlassian's official MCP server.

#### Step 2: Authenticate in Claude Code

1. Open Claude Code (type `claude` in your terminal, or restart if already open)
2. Type `/mcp` and press Enter
3. Select **`atlassian`** from the list
4. Select **"Authenticate"**
5. A browser window will open — log in to your Atlassian account and authorize access

#### Step 3: Test it!

Back in Claude Code, try these queries:

```
What are my open Jira issues?
Search Confluence for "onboarding guide"
```

### What You Can Do

| Tool | Example queries |
|------|----------------|
| **Jira** | "What issues are assigned to me?", "Show my sprint board", "Create a new ticket" |
| **Confluence** | "Find the onboarding doc", "Read page ID 12345", "Search for meeting notes" |

### Troubleshooting

| Problem | Solution |
|---------|----------|
| "Server not found" | Double-check the URL — copy the full command exactly |
| Auth fails | Make sure you're logging into the right Atlassian workspace |
| "No permission" | Ask your admin if API access is enabled |
| Can't find pages | Try using the page ID instead of the title |

## EXECUTE

Follow the 3 steps above:

1. **Terminal:** `claude mcp add --transport http atlassian https://mcp.atlassian.com/v1/mcp`
2. **Claude Code:** `/mcp` → select `atlassian` → Authenticate
3. **Claude Code:** Try `What are my open Jira issues?`

---
👆 Try this yourself now.
When you're done, type "done" or "next" to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "Which connection method do Jira & Confluence use?",
    "header": "Atlassian Quiz",
    "options": [
      {"label": "Plugin", "description": "A one-command install method"},
      {"label": "MCP Server", "description": "A connector added via claude mcp add"},
      {"label": "CLI Tool", "description": "A command-line tool installed separately"}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "MCP Server"

If correct: "Correct! Jira & Confluence connect through an MCP server — different from Slack's plugin approach. The nice thing is one MCP server gives you both Jira and Confluence!"
If incorrect: "Jira & Confluence use the **MCP server** method. Unlike Slack's plugin, you add an MCP server with `claude mcp add`. One connection covers both tools."
