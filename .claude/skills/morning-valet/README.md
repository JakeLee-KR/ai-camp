# Morning Valet

**Your personal morning briefing — one command to start your day.**

Instead of opening Slack, then Jira, then catching up on industry news separately, Morning Valet does all three for you in one go and tells you exactly what to focus on today.

---

## What it does

Type `/morning-valet` and Claude will automatically:

1. **Check your Slack** — shows who mentioned you and what threads need a reply
2. **Check your Jira tickets** — shows what's blocked, in progress, or waiting to be started
3. **Deliver your weekly news** — 5 curated articles relevant to your industry and role
4. **Give you a focus list** — your top 3 priorities for the day, based on what it found

The whole thing takes about 30 seconds and replaces the usual 10–15 minutes of morning tab-switching.

---

## How to use it

Open Claude Code and type:

```
/morning-valet
```

That's it.

---

## First time setup

The very first time you run it, Claude will ask you a few quick questions:

- **For Jira:** Which ticket statuses do you want to hide? (e.g. Done, Closed)
- **For News:** What industry are you in? What's your department?
- **For scheduling:** Do you want this to run automatically every morning?

Answer once — Claude remembers your answers. Every run after that is fully automatic, no questions asked.

---

## What the output looks like

```
Good morning! Today is Wednesday, March 25 2026.
Let's get you ready for the day...

━━━ 📬 SLACK ━━━
🔴 DIRECT MENTIONS (2)
• #qa-team — Sarah, 9:02 AM
  "Jake can you review this test case before standup?"
  👉 Action needed: Reply

━━━ 📋 JIRA ━━━
🟡 IN PROGRESS
• QA-204  Payroll import regression
  👉 Action needed: Continue work

🟢 TO DO
• QA-211  Leave balance edge case
  👉 Action needed: Pick up and start

━━━ 📰 NEWS ━━━
1. 📰 GitHub Copilot now writes Playwright tests automatically
   Source: TechCrunch · Mar 24
   Summary: GitHub announced...

━━━ 🎯 TODAY'S FOCUS ━━━
1. Reply to Sarah's message in #qa-team
2. Continue work on QA-204
3. Pick up QA-211 if time allows

Have a great day! 💪
```

---

## Scheduling it automatically

During first-time setup, say **Yes** to scheduling and pick a time (e.g. "9AM on weekdays"). Claude will set it up so the briefing runs automatically every morning — you just open Claude Code and it's already there.

---

## Skills used inside Morning Valet

Morning Valet is a **skill that chains other skills** together. It calls:

| Skill | What it does |
|---|---|
| `/slack-inbox` | Checks Slack mentions and thread activity |
| `/my-jira-tickets` | Fetches your current sprint tickets |
| `/weekly-news` | Searches for industry news and delivers a digest |

You can also run each of these individually if you only need one section.

---

## Requirements

- Claude Code installed
- Slack connected via MCP
- Jira connected via MCP
- Internet access (for news search)
