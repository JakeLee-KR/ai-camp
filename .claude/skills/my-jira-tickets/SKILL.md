---
name: my-jira-tickets
description: "Check my Jira tickets and show only the ones that need action today. Use for 'my tickets', 'jira check', 'what should I work on', 'check jira', 'my tasks today'."
---

# My Jira Tickets — Daily Action List

## What this skill does
Fetches all Jira tickets assigned to me, filters out completed or closed ones,
excludes QA Ready tickets that I moved to that status myself (already handled),
checks for new comments, and produces a short action-focused list so I know
exactly what to work on today — without having to open Jira manually.

## Inputs needed
- Jira account (via MCP — already connected)
- User filter prefs from `~/.claude/jira-ticket-prefs.json` (optional — loaded automatically)
- No user input required on each run

## Filter preferences (`~/.claude/jira-ticket-prefs.json`)
On first run, if the file does not exist, ask the user these 3 questions. For each question, display the full status list as numbered options so the user can pick by number or type status names.

**Available Jira statuses (show these as options for every question):**
```
 1. Open
 2. Backlog
 3. In Progress
 4. In Review
 5. QA Ready
 6. Release Ready
 7. Released
 8. Done
 9. Closed
10. Cancelled
11. Blocked
```

**Question 1 — Statuses to exclude:**
"Which statuses should be hidden from your list? (pick numbers or type names)"
Default if skipped: `["Done", "Closed", "Cancelled", "Released"]`
Typical choices: Done, Closed, Cancelled, Released (already shipped — no action needed)

**Question 2 — Self-moved statuses to exclude:**
"Which statuses do YOU move tickets to yourself? Those will be auto-hidden. (pick numbers or type names)"
Default if skipped: `["QA Ready"]`
Typical choices: QA Ready, Release Ready (you set these yourself — nothing left to do)
This applies `NOT (status changed to "[status]" by currentUser())` in JQL.

**Question 3 — Must-include statuses:**
"Any statuses you always want to see, even if they'd normally be filtered out? (pick numbers, or press Enter to skip)"
Default if skipped: `[]`
Example: pick `In Review` if you want to track tickets under peer review

Save to `~/.claude/jira-ticket-prefs.json`:
```json
{
  "exclude_statuses": ["Done", "Closed", "Cancelled", "Released"],
  "exclude_self_moved": ["QA Ready"],
  "must_include_statuses": []
}
```

On subsequent runs, load silently — no questions asked. User can say "change my Jira filters" to update.

**When running inside `/morning-valet`:** If the prefs file does not exist, use defaults silently without asking any questions. Save the defaults file automatically so future runs are also silent:
```json
{
  "exclude_statuses": ["Done", "Closed", "Cancelled", "Released"],
  "exclude_self_moved": ["QA Ready"],
  "must_include_statuses": [],
  "setup_complete": true
}
```

## Steps
1. Load prefs from `~/.claude/jira-ticket-prefs.json`. If missing, run first-time setup above.
2. Build JQL dynamically from prefs:
   - Base: `assignee = currentUser() AND sprint in openSprints()`
   - Exclude statuses: `AND status NOT IN ([exclude_statuses])`
   - Exclude self-moved: `AND NOT (status changed to "[status]" by currentUser())` for each item in `exclude_self_moved`
   - Must-include: append `OR status IN ([must_include_statuses])` if set
   - Final: `ORDER BY updated DESC`
   - Example output: `assignee = currentUser() AND sprint in openSprints() AND status NOT IN (Done, Closed, Cancelled) AND NOT (status changed to "QA Ready" by currentUser()) ORDER BY updated DESC`
3. Group tickets by status in this order:
   - 🔴 **BLOCKED** — status is Blocked
   - 🔵 **WAITING FOR YOUR ACTION** — status is QA Ready (moved by someone else), In Review (peer review needed), or any status in `must_include_statuses` where you are the assignee and did not move it there yourself. These are tickets explicitly waiting for YOU to act on them.
   - 🟡 **IN PROGRESS** — status is In Progress
   - 🟢 **TO DO / BACKLOG** — status is Open or Backlog
   - ⏳ **RELEASE READY** — collapsed summary only
4. For each ticket, check the latest comment — flag if there is a comment from someone else waiting for a response
5. Sort within each group by last updated date (most recent first)
6. Format and display tickets by group; show Release Ready as a collapsed summary
   - For ticket links, always use the `webUrl` field from the Jira API response — never construct URLs manually

## Output format

```
📋 My Jira Tickets — {today's date}
{N} tickets need your attention

🔴 BLOCKED
• [TICKET-ID] Title of ticket
  Status: Blocked | Latest comment: "{comment snippet}" — {commenter}, {date}
  🔗 [TICKET-ID](webUrl from Jira response)
  👉 Action needed: Respond to comment / Unblock dependency

🟡 IN PROGRESS
• [TICKET-ID] Title of ticket
  Status: In Progress | No new comments
  🔗 [TICKET-ID](webUrl from Jira response)
  👉 Action needed: Continue work

🔵 WAITING FOR YOUR ACTION
• [TICKET-ID] Title of ticket
  Status: QA Ready | Moved by: {name}, {date}
  🔗 [TICKET-ID](webUrl from Jira response)
  👉 Action needed: Ready to test

🟢 TO DO / BACKLOG
• [TICKET-ID] Title of ticket
  Status: Backlog | Updated: {date}
  🔗 [TICKET-ID](webUrl from Jira response)
  👉 Action needed: Pick up and start

---
⏳ RELEASE READY — {N} tickets waiting for release (no action needed)
✅ {N} tickets are Done/Closed/Released — nothing to do there.
```

## Error handling
- If Jira MCP is not connected: tell the user "Jira is not connected. Please check your MCP settings in Claude Desktop."
- If no tickets are assigned to me: output "No open tickets assigned to you right now. Enjoy the peace! ☀️"
- If ticket comments cannot be retrieved: show the ticket without comment info and note "Comments unavailable"
- If assignee lookup fails: ask the user "What is your Jira username or email?" and retry
