---
name: init-morning-valet
description: "First-time setup for all morning-valet skills. Seeds all prefs files so subsequent runs are fully automatic. Use for 'set up', 'initialize', 'first time setup', 'configure my skills'."
---

# Init Morning Valet

## Steps

**Step 1: Check what's already configured**
Check `~/.claude/morning-valet-prefs.json` (if it doesn't exist yet, treat it as not configured).
Then check whether it contains `"setup_complete": true`.

If it does, print:
```
🔄 Reconfiguring your morning-valet preferences. Your previous settings will be overwritten.
```
Always continue to Step 2 — never skip setup, even if already configured.

**Step 2: Ask setup questions**
Use AskUserQuestion — first call:
- Q1: "Which industry are you in?"
  Options:
  - SaaS / B2B Software
  - FinTech / Finance
  - HealthTech / Healthcare
  - E-commerce / Retail
  - EdTech / Education
  - HR Tech / People Ops
  - Logistics / Supply Chain
  - Other (let them type their own)
- Q2: "What's your department?"
  Options:
  - CEO / Executive
  - Sales
  - Marketing
  - Customer Success (CS)
  - Engineering
  - Product Management (PM)
  - QA

Second AskUserQuestion call:
- Q3: "Which Jira statuses do you want to hide?" (multiSelect: true)
  Options:
  - Open
  - Backlog
  - In Progress
  - In Review
  - QA Ready
  - Release Ready
  - Released
  - Done
  - Closed
  - Cancelled
  - Blocked

**Step 3: Write all three prefs files**
For `weekly-news-prefs.json` and `jira-ticket-prefs.json`: if the file already exists, **merge** the new fields into the existing content, preserving any previously saved values.

For `morning-valet-prefs.json`: **always write fresh** — do not preserve any existing fields. This resets `schedule_asked` so that `/morning-valet` will ask the scheduling question again on the next run.

`~/.claude/weekly-news-prefs.json` — merge these fields:
```json
{ "industry": "[Q1 answer]", "department": "[Q2 answer]", "setup_complete": true }
```

`~/.claude/jira-ticket-prefs.json` — merge these fields:
```json
{
  "exclude_statuses": ["[Q3 selections]"],
  "exclude_self_moved": ["QA Ready"],
  "must_include_statuses": [],
  "setup_complete": true
}
```

`~/.claude/morning-valet-prefs.json` — **overwrite entirely** (do not preserve old fields):
```json
{ "setup_complete": true }
```

**Step 4: Confirm**
```
✅ All set!
  • Industry: [Q1]
  • Department: [Q2]
  • Hidden Jira statuses: [Q3]

Run /morning-valet to start your day.
```

## Error handling
- If a file write fails: show the exact content so the user can create it manually.
