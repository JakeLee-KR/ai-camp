---
name: slack-inbox
description: "Check unread Slack messages — direct mentions and active channels/threads. Use for 'check slack', 'slack inbox', 'what did I miss', 'any mentions', 'unread messages'."
---

# Slack Inbox Check

## What this skill does
Scans Slack for two categories of messages you haven't read:
1. **Direct mentions** — messages where someone @mentioned you by name
2. **Channel & thread activity** — channels or threads you're part of that have new messages

Gives you a prioritized list so you know exactly who needs a reply and what you can catch up on later.

## Inputs needed
- Slack account (via MCP — already connected)
- No user input required on each run

## Steps

**Step 1: Fetch direct mentions**
Search Slack for messages that mention the current user directly.
Use the Slack MCP search tool with query: `@[current_user_display_name]`
Limit to results from the last 24 hours (or last 48 hours on Mondays to catch weekend messages).

**Step 2: Fetch active channel/thread messages**
For each channel the user is a member of, check for recent messages the user has not yet replied to.
Focus on:
- Threads the user participated in that have new replies
- Channels where the user's name or work is referenced
Use the Slack MCP `slack_get_channel_history` or `slack_search_public_and_private` tools.
Limit to the last 24 hours (or 48 hours on Mondays).

**Step 3: Deduplicate**
If a message appears in both mentions and channel activity, show it only once under "Mentions".

**Step 4: Classify each message**
Use these exact rules:

- **Action needed** → someone @mentioned the current user directly by name or user ID in the message body. They are waiting for a response.
- **FYI (cc)** → the current user was not directly @mentioned, but is in the channel or thread where this message appeared (e.g. they were cc'd by being a thread participant, or it's a channel they're in). No reply expected but worth knowing.

**Step 5: Format and display**

## Output format

```
📬 Slack Inbox — {today's date, HH:MM}

🔴 DIRECT MENTIONS ({N})
• #{channel} — {sender_name}, {time}
  "{message snippet}"
  👉 Action needed: Reply — @mentioned directly

• #{channel} — {sender_name}, {time}
  "{message snippet}"
  📌 FYI (cc) — no reply needed

---
💬 CHANNEL & THREAD ACTIVITY ({N})
• #{channel} / 🧵 thread by {original_poster}, {time}
  Latest: "{message snippet}" — {sender_name}
  👉 Action needed: Reply — @mentioned directly

• #{channel}, {time}
  "{message snippet}" — {sender_name}
  📌 FYI (cc)

---
✅ Nothing else unread. You're all caught up!
```

## Error handling
- If Slack MCP is not connected: "Slack is not connected. Please check your MCP settings in Claude Desktop."
- If no mentions found: show "No direct mentions in the last 24 hours. 🎉"
- If no channel activity: show "No new channel or thread activity."
- If both empty: "All clear! No unread Slack messages. 🧘"
- If search returns too many results (>20): show the 10 most recent and note "Showing 10 most recent — {N} total unread"
