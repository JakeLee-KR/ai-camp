# Block 5: Connect HubSpot (Optional)

## EXPLAIN

HubSpot is **optional** — only do this block if your team uses HubSpot for CRM, marketing, or sales. This uses the HubSpot MCP server with OAuth authentication.

### Step-by-Step Guide

#### Step 1: Add the HubSpot MCP server

In Claude Code, run this query (requires Atlassian connection from Block 3):

```
Execute the following command filling out the credentials from confluence document ID: 4733566984
MCP_CLIENT_SECRET={CLIENT_SECRET} claude mcp add --transport http \
  --client-id {CLIENT_ID} --callback-port 6274 --client-secret \
  hubspot https://mcp.hubspot.com/
```

Claude will read the Confluence document, extract the credentials, and run the command with the actual values filled in.

#### Step 2: Restart Claude Code

After adding the MCP server, exit and restart Claude Code:

```
/exit
```

Then in your Terminal:

```bash
claude
```

#### Step 4: Authenticate with HubSpot

1. Type `/mcp` and press Enter
2. Select **`hubspot`** from the list
3. Select **"Authenticate"**
4. A browser window will open:
   - Select **"Swingvy (9014681)"** as the account
   - Select **all optional scopes**
   - Click the checkbox to activate the "Connect app" button
   - Click **"Connect app"**

#### Step 4: Test it!

Back in Claude Code, try these queries:

```
Show me my recent HubSpot contacts
List deals in the pipeline
```

### What You Can Do

| HubSpot Area | Example queries |
|--------------|----------------|
| **CRM** | "Find contact John Smith", "Show recent deals" |
| **Contacts** | "List contacts added this week", "Search for company X" |
| **Deals** | "What deals are in the pipeline?", "Show deals closing this month" |
| **Marketing** | "Show recent HubSpot campaigns", "What's the open rate on our last campaign?" |

### Troubleshooting

| Problem | Solution |
|---------|----------|
| MCP add command fails | Double-check the CLIENT_ID and CLIENT_SECRET from the Confluence doc |
| Auth page won't open | Copy the URL from terminal and paste in your browser |
| "Unauthorized" | Re-authenticate via `/mcp` → hubspot → Authenticate |
| Can't access data | Your HubSpot role may not have API permissions — check with admin |
| Wrong account selected | Make sure to select "Swingvy (9014681)" during OAuth |

## EXECUTE

Follow the 4 steps above:

1. **Claude Code:** Ask Claude to read Confluence doc 4733566984 and run the `claude mcp add` command with the credentials
2. **Restart:** `/exit` then `claude`
3. **Claude Code:** `/mcp` → select `hubspot` → Authenticate → select Swingvy (9014681) → select all scopes → Connect app
4. **Claude Code:** Try `Show me my recent HubSpot contacts`

---
👆 Try this yourself now.
When you're done, type "done" or "next" to continue.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "What authentication method does HubSpot use to connect with Claude Code?",
    "header": "HubSpot Quiz",
    "options": [
      {"label": "Username and password", "description": ""},
      {"label": "OAuth browser flow via MCP", "description": ""},
      {"label": "Personal Access Key", "description": ""},
      {"label": "SSH key pair", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "OAuth browser flow via MCP"

If correct: "Exactly! HubSpot uses OAuth — you add it as an MCP server, then authenticate through a browser flow where you select your account and grant permissions. This is the most secure way to connect!"
If incorrect: "HubSpot connects via an **MCP server with OAuth**. You add the MCP server with credentials from Confluence, then authenticate through a browser flow where you select your HubSpot account and grant permissions."
