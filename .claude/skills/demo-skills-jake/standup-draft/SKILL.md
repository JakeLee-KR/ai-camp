---
name: standup-draft
description: "Generate a daily standup draft from Jira and Slack activity. Use for 'standup', 'daily standup', 'write my standup', 'what did I do yesterday', 'scrum update'."
---

# Daily Standup Draft

## What this skill does
Generates a ready-to-paste standup update by pulling what you actually did from
Jira and Slack — no more staring at a blank screen trying to remember yesterday.

## Steps

**Step 1: Fetch all data in parallel**
Fire ALL of the following at the same time — do not wait for one before starting the next:

| Fetch | What to do |
|---|---|
| **Jira yesterday** | JQL: `assignee = currentUser() AND updated >= -1d ORDER BY updated DESC` (use `-3d` on Mondays) |
| **Jira today** | JQL: `assignee = currentUser() AND sprint in openSprints() AND status IN ("In Progress", "To Do", "Open", "Backlog") ORDER BY updated DESC` |
| **Standup thread** | `slack_get_channel_history` on the standup channel, then `slack_read_thread` on yesterday's bot reminder message |
| **Slack blockers** | `slack_search_public_and_private` for direct mentions from yesterday that have no reply from current user |
| **Calendar** | `gcal_list_events` for today 00:00–23:59, filter out all-day, declined, and standup/stand-up/daily-scrum events |

Wait for all fetches to complete, then proceed.

**Step 2: Cross-check yesterday's todos**
From the standup thread, extract the user's "Todo today" items.
- For each item, check if a matching Jira ticket exists in the current sprint (title substring match)
- If no match: flag with `⚠️ "[task]" was in yesterday's todo but has no open Jira ticket — worth creating one?`

**Step 3: Generate the standup draft**
Using all data fetched in Step 1:
Format the output using the team's standup form — 6 sections, bullet points, plain language:

```
📝 Standup Draft — {today's date}

1. Today, I'm [emoji]

2. Done
• [Action verb] [ticket ID] [ticket title]
• (If nothing: leave blank)

3. Delayed
• [ticket ID] [ticket title] — [brief reason]
• (If nothing: leave blank)

4. Todo today
• [ticket ID] [ticket title]
• (If nothing: "No open tickets assigned — check with team.")

5. Blockage
• [ticket ID] [ticket title] — [brief reason]
• (If none: leave blank)

6. ETC
• [HH:MM] [Meeting title] (from Google Calendar)
• [anything else worth mentioning — OOO, notes]
• (If no meetings and nothing else: leave blank)
```

Use plain, natural language. Keep each bullet to one line.
Action verbs to use: Completed, Moved to QA, Reviewed, Fixed, Updated, Started, Commented on, Closed.
For "Today, I'm" — pick an appropriate emoji based on workload (🙂 normal, 😅 busy, 😴 slow day, etc.).

**Step 4: Ask if the user wants to post it**
After showing the draft, ask:
"Post this to Slack? (yes / no — it will be posted to the standup channel)"
- If yes → post the draft as a new message to the standup channel found in Step 3
- If no → display the draft cleanly so the user can copy-paste it themselves

## Output format

```
📝 Standup Draft — Wednesday, March 26 2026

1. Today, I'm 🙂

2. Done
• Moved LV-959 (Story 3-3, termination date modification) to QA Ready
• Completed CS-6050 (Cannot approve payroll - #14470)

3. Delayed

4. Todo today
• LV-968 [QA] Story 3-1b — Re-visit story 1-3
• MP-1587 Regression test (Mobile)

5. Blockage

6. ETC
• 10:00 1:1 with Jinyoung
• 14:00 Backlog refinement

---
Post to Slack? (yes / no)
```

## Error handling
- If Jira MCP is not connected: "Jira is not connected. Writing standup from Slack activity only."
- If no Jira activity found for yesterday: show "No Jira activity recorded yesterday." and continue
- If Slack is not connected: skip the blocker check and the posting option; note "Slack not connected — copy and paste manually."
- If Google Calendar is not connected: skip Step 4 and leave section 6 blank; note "Calendar not connected — add meetings manually."
- If it's Monday: automatically look back to Friday and note "(Friday's activity)" next to yesterday's items
