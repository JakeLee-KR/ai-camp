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
1. /morning-valet:  orchestrates the full morning briefing and daily focus summary
2. /slack-inbox:    fetches direct mentions and unread channel/thread activity
3. /my-jira-tickets: lists current sprint tickets grouped by status with clickable links
4. /weekly-news:    delivers 5 personalized news items by industry + department via Slack DM
MCP CONNECTIONS NEEDED:
- Slack:  to read mentions, threads, and send the news digest as a DM
- Jira:   to fetch assigned tickets and filter by sprint/status
- WebSearch: to find live news articles from the past 7 days

SUCCESS = I can type /morning-valet and get a full briefing — Slack, Jira,
          and news — with my top 3 priorities for the day, in under 60 seconds.
```

---

## Skills in this repo

| Skill | Command | What it does |
|---|---|---|
| Morning Valet | `/morning-valet` | Runs Slack, Jira, and news briefing in sequence with a daily focus summary |
| Slack Inbox | `/slack-inbox` | Shows direct mentions and unread channel/thread activity |
| My Jira Tickets | `/my-jira-tickets` | Lists your current sprint tickets grouped by status |
| Weekly News | `/weekly-news` | Delivers 5 personalized news items based on your industry and department |
| Daily Checklist | `/daily-checklist` | Shows a day-of-week task checklist to structure your day |
