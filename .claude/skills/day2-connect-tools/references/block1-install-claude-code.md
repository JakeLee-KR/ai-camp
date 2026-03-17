# Block 1: Install Claude Code in Claude Desktop App

## EXPLAIN

Before we connect any tools, we need **Claude Code** running. Claude Code is the powerful engine inside your Claude Desktop App that can connect to external tools, run commands, and automate your work.

### What is Claude Code?

In Day 1, you used the **Claude Desktop App** to have conversations. Claude Code is a **feature inside the Desktop App** that gives you access to powerful capabilities like:

- `/mcp` — manage tool connections
- Plugins — install connectors (like Slack)
- MCP servers — connect to tools (like Jira, HubSpot)
- CLI tools — work with services (like Google Workspace)

### How to Install Claude Code in Desktop App

#### Step 1: Open Claude Desktop App

Launch the Claude Desktop App you installed on Day 1.

#### Step 2: Enable Claude Code

In the Claude Desktop App:
1. Click on **Claude Code** in the bottom-left corner (or look for a terminal icon)
2. Follow the prompts to enable Claude Code
3. You may need to grant Terminal access permissions

> If you don't see the Claude Code option, make sure your Desktop App is up to date. Go to **claude.ai/download** and reinstall the latest version.

#### Step 3: Verify it's working

Once Claude Code is enabled, you should be able to type commands like `/mcp` in your Claude Desktop App chat. Try it!

### Why Do We Need This?

| Feature | Claude Desktop App alone | With Claude Code enabled |
|---------|------------------------|-------------------------|
| Chat with Claude | Yes | Yes |
| Connect external tools (Slack, Jira, etc.) | No | Yes |
| Install plugins | No | Yes |
| Run terminal commands | No | Yes |
| Build skills & automations | Limited | Yes |

### Need Terminal for Some Steps

Some tool connections require running commands in the **Terminal** app. Don't worry — we'll guide you through each step. When Terminal is needed, we'll clearly label it:

```
📱 Desktop App: things you do in Claude Desktop App
💻 Terminal: things you do in the Terminal app
```

## EXECUTE

1. **Open Claude Desktop App**
2. **Enable Claude Code** — look for the Claude Code option in the bottom-left
3. **Test it** — type `/mcp` in your chat to see if Claude Code is working

If you see the MCP management screen (even if it's empty), you're ready to connect tools!

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "Where do you enable Claude Code?",
    "header": "Install Quiz",
    "options": [
      {"label": "In the Claude Desktop App (bottom-left corner)", "description": ""},
      {"label": "By downloading a separate application", "description": ""},
      {"label": "Through your web browser at claude.ai", "description": ""},
      {"label": "In your computer's System Settings", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "In the Claude Desktop App (bottom-left corner)"

If correct: "That's right! Claude Code lives inside the Claude Desktop App. Once enabled, you get access to tool connections, plugins, and all the powerful features we'll use today."
If incorrect: "Claude Code is enabled inside the **Claude Desktop App** itself — look for it in the bottom-left corner. It's not a separate download. Once enabled, you can use commands like `/mcp` to manage tool connections."
