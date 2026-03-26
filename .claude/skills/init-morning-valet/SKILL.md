---
name: init-morning-valet
description: "First-time setup for all morning-valet skills. Seeds all prefs files so subsequent runs are fully automatic. Use for 'set up', 'initialize', 'first time setup', 'configure my skills'."
---

# Init Morning Valet

## Steps

**Step 1: Check what's already configured**
Read `~/.claude/morning-valet-prefs.json` and check whether it contains `"schedule_asked": true`.

If it does, print:
```
🔄 Reconfiguring your morning-valet preferences. Your previous settings will be overwritten.
```
Always continue to Step 2 — never skip setup, even if already configured.

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
