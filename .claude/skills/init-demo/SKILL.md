---
name: init-demo
description: "First-time setup for all morning-valet skills. Seeds all prefs files so subsequent runs are fully automatic. Use for 'set up', 'initialize', 'first time setup', 'configure my skills'."
---

# Init Demo

## Steps

**Step 1: Check what's already configured**
Check which prefs files already exist:
- `~/.claude/morning-valet-prefs.json`
- `~/.claude/jira-ticket-prefs.json`
- `~/.claude/weekly-news-prefs.json`

If all three exist, print:
```
✅ You're already set up! Run /morning-valet to start your day.
```
Then stop.

**Step 2: Ask setup questions**
Use AskUserQuestion — first call:
- Q1: "Which industry are you in?"
  Options: HR Tech / SaaS | Fintech | Enterprise Software | E-commerce / Retail
- Q2: "What's your department?"
  Options: QA | Engineering | Product | CS / Support

Second AskUserQuestion call:
- Q3: "Which Jira statuses do you want to hide?" (multiSelect: true)
  Options: Done | Closed | Cancelled | Released

**Step 3: Write all three prefs files**

`~/.claude/weekly-news-prefs.json`:
```json
{ "industry": "[Q1 answer]", "department": "[Q2 answer]", "setup_complete": true }
```

`~/.claude/jira-ticket-prefs.json`:
```json
{
  "exclude_statuses": ["[Q3 selections]"],
  "exclude_self_moved": ["QA Ready"],
  "must_include_statuses": [],
  "setup_complete": true
}
```

`~/.claude/morning-valet-prefs.json`:
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
