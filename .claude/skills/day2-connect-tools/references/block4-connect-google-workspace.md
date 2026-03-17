# Block 4: Connect Google Workspace

## EXPLAIN

Google Workspace (Calendar, Drive, Docs, Sheets, Gmail) uses a different approach — a **CLI tool** called `gws`. This requires a few more steps in Terminal, but once set up, it gives Claude access to all your Google tools at once.

### Step-by-Step Guide

#### Step 1: Create the client_secret.json file

📱 **Desktop App:** Type this query (requires Atlassian connection from Block 3):

```
create ~/.config/gws/client_secret.json file from confluence document ID: 4734844930
```

This fetches the Google OAuth credentials needed for authentication.

#### Step 2: Install prerequisites

💻 **Terminal:** You need Homebrew and Node.js. Open your Terminal app and run these commands one by one:

```bash
# Install Homebrew (Mac package manager) — skip if you already have it
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```bash
# Install Node.js — skip if you already have it
brew install node
```

To check if you already have them:
```bash
brew --version    # Should show a version number
node --version    # Should show a version number (v18 or higher)
```

#### Step 3: Install the Google Workspace CLI

💻 **Terminal:**

```bash
npm install -g @googleworkspace/cli
```

#### Step 4: Add as a Claude Code skill

💻 **Terminal:**

```bash
npx skills add https://github.com/googleworkspace/cli -y
```

#### Step 5: Authenticate with Google

💻 **Terminal:**

```bash
gws auth login
```

It will first ask you to select an OAuth scope. **Just press Enter** to confirm the recommended setting.

Then it will display a URL. **Copy the URL and open it in your browser.** Log in with your Google account and authorize access.

#### Step 6: Test it in Claude Desktop App!

📱 **Desktop App:** Go back to your Claude Desktop App (restart it if needed) and try:

```
What's my upcoming schedule?
```

If Claude shows your Google Calendar events — Google Workspace is connected!

### What You Can Do

| Google Tool | Example queries |
|-------------|----------------|
| **Calendar** | "What's my schedule tomorrow?", "Block 2-3pm for deep work" |
| **Drive** | "List my recent files", "Find the Q1 report" |
| **Docs** | "Create a meeting notes document", "Read the onboarding doc" |
| **Sheets** | "Open my tracking spreadsheet", "Add a row to the budget sheet" |
| **Gmail** | "Show my unread emails", "Draft a reply to..." |

### Troubleshooting

| Problem | Solution |
|---------|----------|
| `brew` not found | Run the Homebrew install command from Step 2 |
| `node` version too old | `brew upgrade node` |
| `npm install` fails | Try `sudo npm install -g @googleworkspace/cli` |
| Auth URL won't open | Copy the URL manually and paste it in your browser |
| "Permission denied" | Make sure you authorized with the right Google account |
| `client_secret.json` missing | Run Step 1 again in Desktop App to create it from the Confluence doc (requires Block 3 Atlassian connection) |

## EXECUTE

Follow the 6 steps above:

1. 📱 **Desktop App:** `create ~/.config/gws/client_secret.json file from confluence document ID: 4734844930`
2. 💻 **Terminal:** Install Homebrew and Node.js (if not already installed)
3. 💻 **Terminal:** `npm install -g @googleworkspace/cli`
4. 💻 **Terminal:** `npx skills add https://github.com/googleworkspace/cli -y`
5. 💻 **Terminal:** `gws auth login` → copy URL → open in browser → authorize
6. 📱 **Desktop App:** Try `What's my upcoming schedule?`

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "Which connection method does Google Workspace use?",
    "header": "Google Workspace Quiz",
    "options": [
      {"label": "Plugin", "description": "A one-command install method"},
      {"label": "MCP Server", "description": "A connector added via claude mcp add"},
      {"label": "CLI Tool", "description": "A command-line tool installed separately"}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "CLI Tool"

If correct: "Exactly! Google Workspace uses a CLI tool called `gws`. So now you've seen all three methods: Slack = plugin, Atlassian = MCP server, Google = CLI tool. The method doesn't matter much — once connected, you just ask Claude in plain language in your Desktop App."
If incorrect: "Google Workspace uses the **CLI tool** method — a separate tool called `gws` that you install in Terminal and authenticate with. Each tool connects differently (plugin, MCP, CLI), but once connected, you interact with all of them the same way in your Desktop App."
