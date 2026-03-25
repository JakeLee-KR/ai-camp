---
name: morning-valet
description: "Run all morning skills in sequence: Slack inbox, Jira tickets, weekly news digest, and standup draft. Use for 'good morning', 'morning briefing', 'start my day', 'daily briefing', 'morning routine'."
---

# Morning Valet

## What this skill does
Your personal morning briefing. Runs four skills back-to-back and presents a unified summary so you start the day knowing exactly what needs your attention — without switching between tools.

**Order of execution:**
1. 📬 **Slack Inbox** — who mentioned you, what threads are active
2. 📋 **Jira Tickets** — what to work on today
3. 📰 **Weekly News** — what's happening in your industry
4. 📝 **Standup Draft** — ready-to-paste standup for today

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

**Step 1: Open with a greeting**
```
Good morning! 🌅 Today is [Day], [Month DD YYYY].
Let's get you ready for the day. Running your morning briefing...
```

**Step 2: Run Slack Inbox**
Execute the `/slack-inbox` skill in full.
- Fetch direct mentions and channel/thread activity from the last 24h (48h on Mondays)
- Display results under the header: `━━━ 📬 SLACK ━━━`

**Step 3: Run Jira Tickets**
Execute the `/my-jira-tickets` skill in full.
- Load prefs from `~/.claude/jira-ticket-prefs.json`, build JQL, fetch tickets, group by status
- Display results under the header: `━━━ 📋 JIRA ━━━`

**Step 4: Run Weekly News**
Execute the `/weekly-news` skill in full.
- Load prefs from `~/.claude/weekly-news-prefs.json` (industry + department)
- If prefs exist, skip questions and go straight to topic suggestion → search → digest
- Display results under the header: `━━━ 📰 NEWS ━━━`

**Step 5: Run Standup Draft**
Execute the `/standup-draft` skill in full.
- Pull yesterday's Jira activity, today's open tickets, and yesterday's standup thread
- Generate a draft using the 6-section team format
- Display results under the header: `━━━ 📝 STANDUP ━━━`
- Ask: "Post this to the standup channel? (yes / no)"

**Step 6: Close with a daily focus prompt**
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
- On first run, `/weekly-news` may ask for industry + department + schedule preferences. That's expected — it only happens once.
- On first run, `/my-jira-tickets` may ask for filter preferences. That's expected — it only happens once.
- After first-run setup is complete, `/morning-valet` runs fully automatically with no questions.
