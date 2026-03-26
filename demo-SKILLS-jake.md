# Skills

A Claude Code Skill automates a repeatable task using your connected tools.
Use the template below to plan a new skill before building it.

---

## Project Template

```
PROJECT NAME: Morning Valet

PROBLEM (1 sentence):
"Every morning, I spend 10–15 minutes opening Slack, Jira, and news tabs
separately to figure out what needs my attention."

SOLUTION (1 sentence):
"A skill that checks Slack mentions, Jira sprint tickets, and industry news
in one command using Slack, Jira, and WebSearch, saving 10+ minutes every day."

SKILLS I NEED:
1. /morning-valet:   orchestrates the full morning briefing and daily focus summary
2. /slack-inbox:     fetches direct @mentions (action needed) and unread channel/thread activity (FYI cc)
3. /my-jira-tickets: lists current sprint tickets grouped by status with clickable links
4. /weekly-news:     delivers 5 most recent news items by industry + department via Slack DM
5. /standup-draft:   generates a daily standup from Jira, Slack thread, and Google Calendar meetings

MCP CONNECTIONS NEEDED:
- Slack:         read mentions, threads, channels; send news digest as DM
- Jira:          fetch assigned tickets and filter by sprint/status
- Google Calendar: fetch today's meetings for standup section 6 (ETC)
- WebSearch:     find live news articles from the past 7 days

SUCCESS = I can type /morning-valet and get a full briefing — Slack, Jira, news,
          and a ready-to-post standup — with my top 3 priorities, in under 60 seconds.
```

---

## Project Evaluation

| Criterion | Result | Notes |
|---|---|---|
| **6x–10x productivity gap** | ✅ 10–15x | ~15 min morning routine → ~60 seconds with `/morning-valet` |
| **Tasks I couldn't do before** | ✅ New capability | Cross-checking yesterday's standup vs Jira tickets was impossible manually |
| **Good to delegate** | ✅ Perfect fit | Information gathering needs no judgment — Claude assembles, you decide |
| **Worth sharing with team** | ✅ Ready | Works for any Swingvy member with Jira + Slack + Google Calendar connected |
| **Will actually use** | ✅ Already in use | Built from real Jira data, matched to actual standup format |

**Strongest story:** `/standup-draft` + Jira cross-check — flags promised tasks with no open ticket. Unique to a QA workflow, impossible to replicate manually at the same speed.

---

## Skills in this repo

| Skill | Command | What it does |
|---|---|---|
| Morning Valet | `/morning-valet` | Orchestrates Slack, Jira, news, and standup in one briefing with daily focus summary |
| Slack Inbox | `/slack-inbox` | Shows direct @mentions (👉 action needed) and thread/channel activity (📌 FYI cc) |
| My Jira Tickets | `/my-jira-tickets` | Lists current sprint tickets grouped by status with clickable Jira links |
| Weekly News | `/weekly-news` | Delivers 5 most recent news items by industry + department, sent via Slack DM |
| Standup Draft | `/standup-draft` | Generates standup from Jira activity, yesterday's thread, and today's calendar meetings |
| Daily Checklist | `/daily-checklist` | Shows a day-of-week task checklist to structure your day |
