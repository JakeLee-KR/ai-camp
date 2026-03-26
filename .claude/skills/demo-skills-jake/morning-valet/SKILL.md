---
name: morning-valet
description: "Run all morning skills in sequence: Slack inbox, Jira tickets, weekly news digest, and standup draft. Use for 'good morning', 'morning briefing', 'start my day', 'daily briefing', 'morning routine'."
---

# Morning Valet

## What this skill does
Your personal morning briefing. Runs four skills back-to-back and presents a unified summary so you start the day knowing exactly what needs your attention — without switching between tools.

**Execution model: parallel if possible, sequential fallback**
- **If the `Agent` tool is available:** spawn all subagents simultaneously in a single message for ~15–30s total runtime.
- **If the `Agent` tool is not available:** run each section sequentially (Slack → Jira → News → Standup), printing each section header before starting that fetch so the user sees progress.

## First-run setup
On the very first run (check by whether `~/.claude/morning-valet-prefs.json` exists):
Ask: "Would you like your morning briefing delivered automatically on a schedule?"
- Yes → ask: "What time? (e.g. 9AM)" and "Which days? (e.g. weekdays / every day)"
  - Convert to a cron expression and create a scheduled task using `create_scheduled_task`
  - Confirm: "Done! I'll run your morning briefing at [time] on [days]."
- No / Skip → continue without scheduling

Save to `~/.claude/morning-valet-prefs.json`:
```json
{ "setup_complete": true }
```
On subsequent runs, skip this question and go straight to the briefing.

## Steps

**Step 1: Greet + spawn all subagents simultaneously**
Print immediately:
```
Good morning! 🌅 Today is [Day], [Month DD YYYY].
Fetching your briefing... ⏳
```

Then use the `Agent` tool to launch ALL subagents **in a single message** — this is what makes it fast. Never spawn one at a time.

---

**Subagent A — Slack Inbox**
```
Fetch Slack inbox data for the current user.
1. Look up the current user's Slack ID dynamically
2. Search for direct @mentions in the last 24h (48h if today is Monday)
3. Check thread/channel activity for messages the user hasn't replied to
4. Classify each message:
   - Direct @mention in message body → "👉 Action needed: Reply — @mentioned directly"
   - Thread/channel presence, not @mentioned → "📌 FYI (cc)"
Return the complete formatted section starting with: ━━━ 📬 SLACK ━━━
```

**Subagent B — Jira Tickets**
```
Fetch Jira tickets for the current user.
1. Load ~/.claude/jira-ticket-prefs.json — if missing, use silent defaults:
   exclude_statuses: ["Done", "Closed", "Cancelled", "Released"]
   exclude_self_moved: ["QA Ready"]
2. JQL: assignee = currentUser() AND sprint in openSprints() AND status NOT IN ([exclude_statuses]) AND NOT (status changed to "QA Ready" by currentUser()) ORDER BY updated DESC
3. Group by: 🔴 BLOCKED → 🟡 IN PROGRESS → 🟢 TO DO/BACKLOG → ⏳ RELEASE READY
4. Each ticket: 🔗 [TICKET-ID](https://swingvy.atlassian.net/browse/TICKET-ID) Title — Status
Return the complete formatted section starting with: ━━━ 📋 JIRA ━━━
```

**Subagent C — Standup Draft**
```
Generate a standup draft.
1. Fetch in parallel:
   a. Yesterday's Jira: assignee = currentUser() AND updated >= -1d (use -3d on Mondays)
   b. Today's open Jira: assignee = currentUser() AND sprint in openSprints() AND status IN ("In Progress", "To Do", "Open", "Backlog")
   c. Yesterday's standup thread from channel C017BR4KUPL — find the bot reminder message and read the user's reply
   d. Today's Google Calendar events — exclude all-day, declined, and events with "standup"/"stand-up"/"daily scrum" in the title
2. Cross-check yesterday's "Todo today" items against open Jira — flag any with no matching ticket (⚠️)
3. Generate draft in 6-section team format:
   1. Today, I'm [emoji based on workload]
   2. Done  3. Delayed  4. Todo today  5. Blockage
   6. ETC — list calendar meetings as [HH:MM] Title
Return the complete formatted section starting with: ━━━ 📝 STANDUP ━━━
End with an AskUserQuestion: "Post this to the standup channel?" with options "Yes, post it" / "No, I'll copy-paste"
```

**Subagent D — Weekly News (Mondays only)**
```
Only run if today is Monday. If not Monday, return exactly: SKIP
If Monday:
1. Load ~/.claude/weekly-news-prefs.json for saved topic
2. Calculate 7 days ago date. Run 4 parallel searches:
   - [TOPIC] news after:[date]
   - [TOPIC] announcement release after:[date]
   - [TOPIC] tool update case study [year]
   - [TOPIC] site:twitter.com OR site:x.com OR site:threads.net after:[date]
3. Sort all results by publish date, pick 5 most recent
4. If <3 from past 7 days: prefix "📭 Not much this week — most recent items:"
5. If 0–1 results total: return "📭 Nothing special this week."
Return the complete formatted section starting with: ━━━ 📰 NEWS ━━━
```

---

Wait for all subagents to return, then proceed to Step 2.

**If `Agent` tool is NOT available — sequential fallback:**
Run each section one at a time, printing the header before starting each fetch so the user sees progress:
```
━━━ 📬 SLACK ━━━  ← print this, then fetch
[results]
━━━ 📋 JIRA ━━━  ← print this, then fetch
[results]
━━━ 📰 NEWS ━━━  ← Monday only
[results]
━━━ 📝 STANDUP ━━━  ← print this, then fetch
[results]
```

**Step 2: Assemble and display results**
Display sections in order: Slack → Jira → News (skip if Subagent D returned SKIP or if not Monday) → Standup

**Step 6: Close with a daily focus prompt**
Once all sections have arrived, print:
```
━━━ 🎯 TODAY'S FOCUS ━━━
Based on the above, here are your top 3 priorities for today:
1. [Most urgent Slack item or Jira ticket]
2. [Second priority — Jira or Slack]
3. [One thing to keep an eye on]

Have a great day! 💪
```
Derive the top 3 from the actual results — pick the highest-priority Slack mention and Jira tickets. Do not make up items.

## Output format
Sections appear in order: Slack → Jira → News (Mondays only) → Standup → Focus.
Each section is separated by its header line (━━━ emoji TITLE ━━━).

## Error handling
- If a subagent fails or its MCP is disconnected: show an error banner for that section and continue
  ```
  ━━━ 📬 SLACK ━━━
  ⚠️  Slack is not connected. Skipping this section.
  ```
- If all fail: "All tools are currently disconnected. Please check your MCP settings in Claude Desktop."
- Never stop early — always attempt all sections even if one fails
