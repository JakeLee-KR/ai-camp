---
name: morning-valet
description: "Run all morning skills in sequence: Slack inbox, Jira tickets, weekly news digest, and standup draft. Use for 'good morning', 'morning briefing', 'start my day', 'daily briefing', 'morning routine'."
---

# Morning Valet

## What this skill does
Your personal morning briefing. Runs four skills back-to-back and presents a unified summary so you start the day knowing exactly what needs your attention — without switching between tools.

**Execution model: parallel data fetch → sequential display**
All data is fetched in parallel first (like subagents), then results are formatted and displayed in order. This cuts total runtime from ~60s to ~15s.

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

**Step 1: Greet + launch all data fetches in parallel**
Print immediately:
```
Good morning! 🌅 Today is [Day], [Month DD YYYY].
Fetching your briefing... ⏳
```

Then fire ALL of the following in parallel — do not wait for one before starting the next:

| Fetch | What to do |
|---|---|
| **Slack mentions** | Search for direct @mentions of current user, last 24h (48h on Mondays) |
| **Slack channel activity** | Check threads/channels for new messages user hasn't replied to |
| **Jira tickets** | Load `~/.claude/jira-ticket-prefs.json` (use silent defaults if missing), run JQL, fetch tickets |
| **News search** | **Mondays only.** Check today's day of week — if Monday, load `~/.claude/weekly-news-prefs.json` and run 4 parallel searches for the saved topic. If not Monday, skip this fetch entirely. |
| **Standup data** | Fetch: yesterday's Jira activity, today's open Jira tickets, yesterday's standup thread, today's calendar events |

Wait for all fetches to complete before moving to Step 2.

**Step 2: Display Slack results**
Format and print under `━━━ 📬 SLACK ━━━`
- Direct @mentions → `👉 Action needed: Reply`
- Thread/channel presence → `📌 FYI (cc)`

**Step 3: Display Jira results**
Format and print under `━━━ 📋 JIRA ━━━`
- Group by status: 🔴 BLOCKED → 🟡 IN PROGRESS → 🟢 TO DO → ⏳ RELEASE READY
- Each ticket as `🔗 [TICKET-ID](url) Title — Status`

**Step 4: Display News results (Mondays only)**
- If today is **not Monday**: skip this section entirely — do not print the header.
- If today is **Monday**: format and print under `━━━ 📰 NEWS ━━━`
  - 5 most recent items, sorted by date
  - If fewer than 3 from past 7 days: show "📭 Not much this week — here are the most recent:"
  - If 0–1 results: "📭 Nothing special this week."

**Step 5: Display Standup draft**
Format and print under `━━━ 📝 STANDUP ━━━`
- Use the 6-section team format (Today I'm / Done / Delayed / Todo / Blockage / ETC)
- ETC: list today's calendar meetings (exclude standup itself)
- Ask: "Post this to the standup channel? (yes / no)"

**Step 6: Close with a daily focus prompt
After all four sections, print:
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
Each section is separated by a bold header line. Sections appear in order: Slack → Jira → News → Standup → Focus.
Keep each section's output identical to what the individual skill would produce.

## Error handling
- If a skill fails or its MCP is disconnected: show an error banner for that section and continue with the remaining skills
  ```
  ━━━ 📬 SLACK ━━━
  ⚠️  Slack is not connected. Skipping this section.
  ```
- If all four fail: "All tools are currently disconnected. Please check your MCP settings in Claude Desktop."
- Never stop early — always attempt all four skills even if one fails

## Notes
- On first run, `/weekly-news` will ask for industry + department (2 questions only). That's expected — it only happens once.
- On first run, `/my-jira-tickets` uses defaults silently — no questions asked inside morning-valet.
- After first-run setup is complete, `/morning-valet` runs fully automatically with no questions.
- Scheduling is owned by morning-valet only — individual skills should not ask about scheduling when called from here.
