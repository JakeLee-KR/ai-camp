# Block 1: Install Claude Code in Terminal

## EXPLAIN

Before we connect any tools, we need to make sure **Claude Code** is installed in your terminal. The `/mcp` command and plugin installs all require the `claude` CLI to be available.

### What is Claude Code (CLI)?

In Day 1, you may have used the **Claude Desktop App** (the GUI). Claude Code is the **terminal version** — it runs inside your Terminal app and gives you access to powerful features like:

- `/mcp` — manage tool connections
- `claude plugin install` — install plugins (like Slack)
- `claude mcp add` — add MCP servers (like Jira)

### How to Install

#### Step 1: Open your Terminal

On Mac: Press `Cmd + Space`, type "Terminal", and press Enter.

#### Step 2: Install Claude Code

Run this command:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

This downloads and installs Claude Code automatically — no extra dependencies needed.

#### Step 3: Verify the installation

```bash
claude --version
```

You should see a version number like `2.x.x`. If you see it, you're good to go!

#### Step 4: Launch Claude Code

```bash
claude
```

This opens Claude Code in your terminal. You should see a prompt where you can type messages to Claude.

> **To quit Claude Code**, type `/exit` and press Enter.

### Already Installed?

If you already have Claude Code from Day 1, just run the same install command again to update:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

## EXECUTE

Follow the steps above:

1. **Open Terminal**
2. **Install:** `curl -fsSL https://claude.ai/install.sh | bash`
3. **Verify:** `claude --version`
4. **Launch:** `claude`

---
👆 Try this yourself now.
When you're done, type "done" or "next" to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "What command do you use to verify Claude Code is installed correctly?",
    "header": "Install Quiz",
    "options": [
      {"label": "claude --version", "description": "Check the installed version"},
      {"label": "claude --check", "description": "Run a check command"},
      {"label": "which claude", "description": "Find the claude binary location"},
      {"label": "claude status", "description": "Show Claude Code status"}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "claude --version"

If correct: "That's right! `claude --version` shows the installed version number, confirming Claude Code is ready to use."
If incorrect: "The command to verify your installation is `claude --version`. If it shows a version number, you're all set!"
