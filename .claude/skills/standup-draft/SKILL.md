---
name: standup-draft
description: "Generate a daily standup draft from Jira and Slack activity. Use for 'standup', 'daily standup', 'write my standup', 'what did I do yesterday', 'scrum update'."
---

# Daily Standup Draft

## What this skill does
Generates a ready-to-paste standup update by pulling what you actually did from
Jira and Slack — no more staring at a blank screen trying to remember yesterday.

## Steps

**Step 1: Find standup channel + fetch all data in parallel**
First, determine the standup channel:
- Check `~/.claude/morning-valet-prefs.json` for a `standup_channel_id` field — use it if present.
- If not found, search Slack for a channel whose name contains "standup", "stand-up", or "daily" using `slack_search_channels`. Use the best match. Save the ID to `~/.claude/morning-valet-prefs.json` for next time.

Then fire ALL of the following in a single message — do not wait for one before starting the next:

| Fetch | What to do |
|---|---|
| **Jira yesterday** | JQL: `assignee = currentUser() AND updated >= -1d AND status changed DURING (-1d, now()) ORDER BY updated DESC` (use `-3d` on Mondays) |
| **Jira today** | Two queries: (1) `assignee = currentUser() AND sprint in openSprints() AND status NOT IN (Done, Closed, Cancelled, Released, "Release Ready") ORDER BY updated DESC` for in-progress work; (2) `assignee = currentUser() AND sprint in openSprints() AND status = "QA Ready" AND NOT (status changed to "QA Ready" by currentUser()) ORDER BY updated DESC` for tickets moved to QA Ready by others (these go into "Todo today" as items to test) |
| **Slack standup thread** | `slack_get_channel_history` on the standup channel — find the user's message from yesterday (or Friday if Monday), read thread replies |
| **Slack blockers** | `slack_search_public_and_private` for direct mentions from yesterday that have no reply from current user |
| **Calendar** | `gcal_list_events` for today 00:00–23:59, filter out all-day, declined, and standup/stand-up/daily-scrum events |

Wait for all five fetches to complete, then move to Step 2.

**Step 2: Generate the standup draft**
Using all data fetched above:
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
• [ticket ID] [ticket title]  ← in-progress tickets continuing from yesterday
• [ticket ID] [ticket title]  ← QA Ready tickets moved by others (ready to test)
• [HH:MM] [Meeting title]  ← meetings from Google Calendar (same ones as ETC, listed here too)
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
• Test SQ-9871 — Wrong colour of Unpaid leave badge (QA Ready, assigned by Mina)
• 10:30 QA sync up for LPE2
• 15:00 Demo day - Swingvy AI Camp

5. Blockage

6. ETC
• 10:00 1:1 with Jinyoung
• 14:00 Backlog refinement
```

## Error handling
- If Jira MCP is not connected: "Jira is not connected. Writing standup from Slack activity only."
- If no Jira activity found for yesterday: show "No Jira activity recorded yesterday." and continue
- If Slack is not connected: skip the blocker check; note "Slack not connected — copy and paste manually."
- If Google Calendar is not connected: skip Step 4 and leave section 6 blank; note "Calendar not connected — add meetings manually."
- If it's Monday: automatically look back to Friday and note "(Friday's activity)" next to yesterday's items
