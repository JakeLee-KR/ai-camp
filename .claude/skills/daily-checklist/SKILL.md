---
name: daily-checklist
description: "Greet the user with today's date and show a checklist of 5 tasks tailored to the day of the week."
---

# Daily Checklist

## INPUT
- Today's date and day of the week (from system)

## PROCESS

**Step 1: Greet the user**
Print a warm greeting with today's full date:
```
Good morning! Today is [Day], [Month DD YYYY]. Here's your checklist for today 📋
```

**Step 2: Determine the day of the week**
Check today's day and select the matching checklist below.

**Step 3: Show the checklist**
Print the 5 items for today's day (see OUTPUT section).

## OUTPUT

Print the checklist as a numbered list with checkboxes:
```
[ ] 1. Task
[ ] 2. Task
...
```

### Checklists by Day

**Monday — Plan & Align**
1. Review your Jira board and reprioritize tickets for the week
2. Check Slack for any weekend updates or blockers
3. Set your top 3 goals for the week
4. Schedule or confirm any meetings for the week ahead
5. Clear your inbox and flag anything that needs a response today

**Tuesday — Deep Work**
1. Pick your most important ticket and make meaningful progress on it
2. Review any PRs or test cases waiting for your input
3. Update ticket statuses to reflect current progress
4. Check for any new bugs or issues reported overnight
5. Do a quick team sync if anything is blocked

**Wednesday — Mid-week Check**
1. Review progress against your weekly goals — are you on track?
2. Follow up on any comments or questions on your Jira tickets
3. Run or review any pending test cases
4. Identify anything at risk of not completing this week
5. Update your team on your status via Slack

**Thursday — Push & Wrap**
1. Complete or close any tickets you can finish today
2. Review test results and log any new bugs found
3. Prepare notes for any end-of-week meetings
4. Help unblock teammates if they're waiting on you
5. Check if any tickets need status updates before end of week

**Friday — Wrap Up & Reflect**
1. Close out completed tickets and update statuses in Jira
2. Write a brief summary of what you accomplished this week
3. Flag any unfinished items and plan carry-overs for next week
4. Clean up your Slack messages and respond to anything pending
5. Do a quick retrospective: what went well, what could improve?

**Saturday / Sunday — Rest Mode**
1. Step away from work — rest is part of productivity 🌿
2. If you must check in, spend max 15 minutes reviewing urgent messages only
3. Jot down any ideas that came to mind during the week
4. Optional: read one article relevant to your work for inspiration
5. Prepare mentally for Monday — review your top priority for next week

## RULES
- Always use today's actual date and day — never guess or hardcode
- Keep the tone friendly and encouraging
- Print checkboxes as `[ ]` so the user can mentally tick them off
