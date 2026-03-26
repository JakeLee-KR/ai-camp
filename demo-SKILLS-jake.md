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
1. /morning-valet:        orchestrates the full morning briefing and daily focus summary
2. /slack-inbox:           fetches direct @mentions (action needed) and unread channel/thread activity (FYI cc)
3. /my-jira-tickets:       lists current sprint tickets grouped by status with clickable links
4. /weekly-news:           delivers 5 most recent news items by industry + department via Slack DM
5. /standup-draft:         generates a daily standup from Jira, Slack thread, and Google Calendar meetings
6. /init-morning-valet:    first-time setup — seeds all prefs files so subsequent runs are fully automatic

MCP CONNECTIONS NEEDED:
- Slack:             read mentions, threads, channels; send news digest as DM
- Jira:              fetch assigned tickets and filter by sprint/status
- Google Calendar:   fetch today's meetings for standup section 6 (ETC)
- WebSearch:         find live news articles from the past ~30 days (prefer the last 7 days)

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
| Init Morning Valet | `/init-morning-valet` | First-time setup — walks through preference questions and seeds all prefs files so morning-valet runs fully automatically |

---

## Skill Details

### 1. `/morning-valet` — Orchestrator

**Purpose:** One command to start your day. Runs all sub-skills and delivers a unified briefing.

**How it works:**
- **Pre-flight permission check** — before spawning subagents, calls one lightweight tool per integration (Slack, Jira, Calendar) in the main session. This triggers the permission dialog so the user can approve; subagents inherit the session approval and run without interruption. If a tool is denied, that section is skipped gracefully.
- Parallel execution if the `Agent` tool is available (all subagents launch simultaneously, ~15–30s total); sequential fallback otherwise (Slack → Jira → News → Standup).
- First-done, first-served display — sections print as each subagent finishes.
- Closes with **🎯 Today's Focus** — top 3 priorities derived from the actual Slack + Jira results.

**First-run behavior:**
- Checks `~/.claude/morning-valet-prefs.json` for `"schedule_asked": true`.
- If not found (file missing, or created by `/init-morning-valet` without that flag), asks: _"Would you like your morning briefing delivered automatically on a schedule?"_
- After answering, writes `"schedule_asked": true` to the prefs file. Subsequent runs skip the question.

**Sections produced:**

| Section | Sub-skill | When |
|---|---|---|
| 📬 Slack | `/slack-inbox` | Every day |
| 📋 Jira | `/my-jira-tickets` | Every day |
| 📰 News | `/weekly-news` | Mondays only |
| 📝 Standup | `/standup-draft` | Every day |
| 🎯 Focus | (built-in) | Every day |

---

### 2. `/slack-inbox` — Slack Mentions & Activity

**Purpose:** Shows who needs a reply and what you can catch up on later.

**How it works:**
1. Searches Slack for direct @mentions of the current user (last 24h; 48h on Mondays).
2. Checks channels/threads the user participates in for new messages.
3. Deduplicates — if a message is both a mention and channel activity, it appears only under Mentions.
4. Classifies each message:
   - **👉 Action needed** — you were directly @mentioned.
   - **📌 FYI (cc)** — you're in the channel/thread but not directly mentioned.

**Output sections:** `🔴 DIRECT MENTIONS` → `💬 CHANNEL & THREAD ACTIVITY`

---

### 3. `/my-jira-tickets` — Sprint Tickets by Status

**Purpose:** Shows only the tickets that need your action today — no noise.

**How it works:**
1. Loads filter preferences from `~/.claude/jira-ticket-prefs.json` (or asks setup questions on first solo run; uses defaults silently when called from `/morning-valet`).
2. Builds JQL dynamically:
   - Base: `assignee = currentUser() AND sprint in openSprints()`
   - Excludes statuses the user chose to hide (default: Done, Closed, Cancelled, Released)
   - Excludes self-moved statuses (default: QA Ready moved by you = already handled)
   - Includes must-see statuses if configured
3. Groups tickets by priority:

| Group | Meaning |
|---|---|
| 🔴 BLOCKED | Status is Blocked |
| 🔵 WAITING FOR YOUR ACTION | QA Ready (moved by someone else), In Review, or must-include where you didn't move it |
| 🟡 IN PROGRESS | Status is In Progress |
| 🟢 TO DO / BACKLOG | Status is Open or Backlog |
| ⏳ RELEASE READY | Collapsed summary — no action needed |

4. Flags tickets with unread comments from others.
5. Links use `webUrl` from the Jira API — never manually constructed.

---

### 4. `/weekly-news` — Personalized News Digest

**Purpose:** 5 curated news items for your industry + role, delivered to your Slack DM.

**How it works:**
1. Checks `~/.claude/weekly-news-prefs.json` for saved industry/department. If found, asks "Same or change?" If missing, asks the user to pick.
2. Combines industry × department to suggest 3 search topics (e.g. _FinTech + QA → "AI agents for FinTech software testing"_).
3. Runs 4 parallel web searches (news, announcements, tools/case studies, X/Threads posts) for the last ~30 days (while *preferring* the last 7 days).
4. Picks the 5 most recent results. If fewer than 3 of the selected top-5 are from the past week, shows a "not much happened" note (otherwise no extra note). If 0–1 total meaningful results, skips with a "nothing this week" message.
5. Formats each item with headline, source, date, summary, and link. Labels X posts as 🐦 and Threads as 🧵.
6. Closes with a one-sentence takeaway connecting a theme across all 5 items.
7. Sends the full digest as a Slack DM to the current user.

Notes:
- Ensures at least 1 item from X/Threads if available by replacing the least-recent non-X/Threads item in the top-5.
- If Slack DM fails (Slack disconnected / Slack ID lookup fails), it still prints the digest to the terminal and asks the user to copy-paste.

---

### 5. `/standup-draft` — Ready-to-Post Standup

**Purpose:** Generates your daily standup from actual Jira, Slack, and Calendar data — no blank-screen guessing.

**How it works:**
1. Finds the standup channel (cached in prefs, or searches Slack for a channel named "standup"/"daily").
2. Fires all data fetches in parallel:

| Fetch | Source |
|---|---|
| Jira yesterday | Tickets with status changes in the last 1 day (3 days on Monday) |
| Jira today | Open sprint tickets not Done/Closed/Cancelled/Released |
| Slack standup thread | User's message from yesterday + thread replies |
| Slack blockers | Direct mentions with no reply from current user |
| Calendar | Today's events (excludes all-day, declined, standup-like meetings) |

3. Maps data into the team's 6-section format:

```
1. Today, I'm [emoji]
2. Done       — completed/moved tickets
3. Delayed    — tickets behind schedule + reason
4. Todo today — open tickets to work on
5. Blockage   — blocked tickets + reason
6. ETC        — meetings from calendar + other notes
```

4. Outputs a standup draft in the team's format so you can copy-paste (no additional yes/no prompts).

---

### 6. `/init-morning-valet` — First-Time Setup

**Purpose:** Interactive setup wizard that seeds all preference files so every subsequent `/morning-valet` run is fully automatic.

**How it works:**
1. Reads `~/.claude/morning-valet-prefs.json` and checks for `"schedule_asked": true`. If found, prints a "Reconfiguring" notice. Always continues to setup regardless.
2. Asks 3 questions:
   - Q1: Industry (SaaS / B2B Software, FinTech / Finance, HealthTech / Healthcare, E-commerce / Retail, EdTech / Education, HR Tech / People Ops, Logistics / Supply Chain, Other)
   - Q2: Department (CEO / Executive, Sales, Marketing, Customer Success (CS), Engineering, Product Management (PM), QA)
   - Q3: Jira statuses to hide (multiSelect; default Done, Closed, Cancelled, Released; options include Open, Backlog, In Progress, In Review, QA Ready, Release Ready, Released, Done, Closed, Cancelled, Blocked)
3. Writes 3 prefs files:
   - `~/.claude/weekly-news-prefs.json` — industry + department
   - `~/.claude/jira-ticket-prefs.json` — excluded statuses + self-moved defaults
   - `~/.claude/morning-valet-prefs.json` — `setup_complete: true`
4. Confirms with a summary of all saved preferences.

---

## Architecture

```
/init-morning-valet          (one-time setup wizard)
        │
        ▼  writes prefs files
┌──────────────────┐
│ morning-valet-   │   jira-ticket-    weekly-news-
│ prefs.json       │   prefs.json      prefs.json
└──────┬───────────┘
       │
       ▼  reads prefs + orchestrates
/morning-valet
       │
       ▼  Step 0: pre-flight (main session)
       ├──→ slack_search_channels   ← triggers Slack permission prompt
       ├──→ atlassianUserInfo       ← triggers Jira permission prompt
       ├──→ gcal_list_calendars     ← triggers Calendar permission prompt
       │    (user approves each → session-wide approval inherited by subagents)
       │
       ▼  Step 1: subagents (parallel)
       ├──→ /slack-inbox        (Slack MCP)
       ├──→ /my-jira-tickets    (Jira MCP + jira-ticket-prefs.json)
       ├──→ /weekly-news        (WebSearch + weekly-news-prefs.json, Mondays)
       ├──→ /standup-draft      (Jira + Slack + Google Calendar MCP)
       │
       └──→ 🎯 Today's Focus   (derived from all results)
```
