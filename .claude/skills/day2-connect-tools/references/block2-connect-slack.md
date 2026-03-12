# Block 1: Connect Slack

## EXPLAIN

Let's connect your first tool — **Slack**. This is the easiest one because it uses a simple plugin install.

### Step-by-Step Guide

#### Step 1: Install the Slack plugin

In your **Terminal** (outside Claude Code), run:

```bash
claude plugin install slack
```

This downloads and sets up the Slack connector automatically.

#### Step 2: Authenticate in Claude Code

1. Open Claude Code (type `claude` in your terminal)
2. Type `/mcp` and press Enter
3. Select **`plugin:slack:slack`** from the list
4. Select **"Authenticate"**
5. A browser window will open — log in to your Slack workspace and authorize access

#### Step 3: Test it!

Back in Claude Code, try this query:

```
What's the most recent message in #swingvy_general?
```

If Claude reads your Slack channel and shows you the message — congratulations, Slack is connected!

### Troubleshooting

| Problem | Solution |
|---------|----------|
| Plugin install fails | Check your internet connection, try again |
| Authentication page won't open | Copy the URL from terminal and paste in your browser |
| "Channel not found" | Check the exact channel name (case-sensitive) |
| Can't read messages | You may need to be a member of that channel |

### Useful Commands

```bash
claude mcp list          # Verify Slack appears in the list
claude mcp remove <name> # Remove if you need to start over
```

## EXECUTE

Follow the 3 steps above:

1. **Terminal:** `claude plugin install slack`
2. **Claude Code:** `/mcp` → select `plugin:slack:slack` → Authenticate
3. **Claude Code:** Try `What's the most recent message in #swingvy_general?`

---
👆 Try this yourself now.
When you're done, type "done" or "next" to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "Which connection method does Slack use?",
    "header": "Slack Quiz",
    "options": [
      {"label": "Plugin", "description": "A one-command install method"},
      {"label": "MCP Server", "description": "A connector added via claude mcp add"},
      {"label": "CLI Tool", "description": "A command-line tool installed separately"}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "Plugin"

If correct: "Right! Slack uses the plugin method — the simplest way to connect a tool. Just one command to install, then authenticate through `/mcp`."
If incorrect: "Slack uses the **plugin** method — it's the easiest of the three. Plugins are one-command installs that handle all the setup for you."
