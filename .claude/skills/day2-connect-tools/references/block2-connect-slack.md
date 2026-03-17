# Block 2: Connect Slack

## EXPLAIN

Let's connect your first tool — **Slack**. This is the easiest one because it uses a simple plugin install.

### Step-by-Step Guide

#### Step 1: Install the Slack plugin

💻 **Terminal:** Open your Terminal app and run:

```bash
claude plugin install slack
```

This downloads and sets up the Slack connector automatically.

#### Step 2: Authenticate in Claude Desktop App

📱 **Desktop App:**
1. Go back to your Claude Desktop App
2. Type `/mcp` and press Enter
3. Select **`plugin:slack:slack`** from the list
4. Select **"Authenticate"**
5. A browser window will open — log in to your Slack workspace and authorize access

#### Step 3: Test it!

📱 **Desktop App:** Try this query:

```
What's the most recent message in #swingvy_general?
```

If Claude reads your Slack channel and shows you the message — congratulations, Slack is connected!

### Troubleshooting

| Problem | Solution |
|---------|----------|
| Plugin install fails | Check your internet connection, try again |
| Authentication page won't open | Copy the URL and paste in your browser |
| "Channel not found" | Check the exact channel name (case-sensitive) |
| Can't read messages | You may need to be a member of that channel |

### Useful Commands

💻 **Terminal:** You can manage connections from Terminal if needed:

```bash
claude mcp list          # Verify Slack appears in the list
claude mcp remove <name> # Remove if you need to start over
```

## EXECUTE

Follow the 3 steps above:

1. 💻 **Terminal:** `claude plugin install slack`
2. 📱 **Desktop App:** `/mcp` → select `plugin:slack:slack` → Authenticate
3. 📱 **Desktop App:** Try `What's the most recent message in #swingvy_general?`

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

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

If correct: "Right! Slack uses the plugin method — the simplest way to connect a tool. Just one command to install, then authenticate through `/mcp` in your Desktop App."
If incorrect: "Slack uses the **plugin** method — it's the easiest of the three. Plugins are one-command installs that handle all the setup for you."
