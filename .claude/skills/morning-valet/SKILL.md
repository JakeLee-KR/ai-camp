---
name: morning-valet
description: "Run all morning skills in sequence: Slack inbox, Jira tickets, weekly news digest, and standup draft. Use for 'good morning', 'morning briefing', 'start my day', 'daily briefing', 'morning routine'."
---

# Morning Valet

## What this skill does
Your personal morning briefing. Runs four skills back-to-back and presents a unified summary so you start the day knowing exactly what needs your attention — without switching between tools.

**Execution model: parallel if possible, sequential fallback**
- **If the `Agent` tool is available:** spawn all subagents simultaneously in a single message for ~15–30s total runtime.
- **If the `Agent` tool is not available:** run each section sequentially (Slack → Jira → News → Standup), printing each section header before starting that fetch so the user sees progress.

## First-run setup
On the very first run (check by whether `~/.claude/morning-valet-prefs.json` contains `"schedule_asked": true`):
- If `schedule_asked` is NOT true (including when the file doesn't exist or was created by `/init-morning-valet`), ask the scheduling question.
- If `schedule_asked` is true, skip straight to the briefing.

Ask: "Would you like your morning briefing delivered automatically on a schedule?"
- Yes → ask: "What time? (e.g. 9AM)" and "Which days? (e.g. weekdays / every day)"
  - Convert to a cron expression and create a scheduled task using `create_scheduled_task`
  - Confirm: "Done! I'll run your morning briefing at [time] on [days]."
- No / Skip → continue without scheduling

After asking (regardless of answer), update `~/.claude/morning-valet-prefs.json` to add `"schedule_asked": true`. Preserve any existing fields (e.g. `setup_complete`).
On subsequent runs, skip this question and go straight to the briefing.

## Steps

**Step 0: Pre-flight — obtain tool permissions before spawning subagents**
Subagents run headlessly and cannot show permission prompts. To avoid silent failures,
call one lightweight tool from each integration in the main session first. This triggers
the permission dialog so the user can approve, and subagents inherit the session approval.

Make these calls (errors are fine — the goal is to trigger the prompt, not get data):
- **Slack:** call `slack_search_channels` with query `"standup"`
- **Jira:** call `atlassianUserInfo` with no arguments
- **Google Calendar:** call `gcal_list_calendars` with no arguments

Print before calling:
```
🔐 Checking tool permissions... (approve each prompt to continue)
```

If a tool is denied by the user: show a warning for that section and skip it.
If a tool is approved (or already was): continue normally.
After all three checks, proceed to Step 1.

**Step 1: Greet + spawn all subagents simultaneously**
Print immediately:
```
Good morning! 🌅 Today is [Day], [Month DD YYYY].
Fetching your briefing... ⏳
```

The base directory for this skill is shown at the top of this skill run (e.g. `/path/to/.claude/skills/demo-skills-jake`). Sub-skill files are siblings in that same directory — read them directly using that path. Never search for them.

**If the `Agent` tool is available:** launch ALL four subagents in a single message using the Agent tool. Pass each subagent the full contents of its SKILL.md as the prompt, read from:
- `{base_dir}/slack-inbox/SKILL.md` → Subagent A (model: opus)
- `{base_dir}/my-jira-tickets/SKILL.md` → Subagent B (model: opus)
- `{base_dir}/standup-draft/SKILL.md` → Subagent C (model: opus)
- `{base_dir}/weekly-news/SKILL.md` → Subagent D (model: opus, only if today is Monday)

**First-done, first-served display:** Do NOT wait for all subagents before showing output. As each subagent returns its result, immediately print that section with its header — in whatever order they finish. After all sections have been printed, proceed to Step 2.

**If `Agent` tool is NOT available — sequential fallback:**
Read each SKILL.md directly using the base directory path and execute sequentially, printing each header before starting that fetch:
```
━━━ 📬 SLACK ━━━  ← print this, then execute slack-inbox/SKILL.md
[results]
━━━ 📋 JIRA ━━━  ← print this, then execute my-jira-tickets/SKILL.md
[results]
━━━ 📰 NEWS ━━━  ← Monday only, execute weekly-news/SKILL.md
[results]
━━━ 📝 STANDUP ━━━  ← print this, then execute standup-draft/SKILL.md
[results]
```

**Step 2: Close with a daily focus prompt**
Once all sections have arrived, print:
```
━━━ 🎯 TODAY'S FOCUS ━━━
Based on the above, here are your top 3 priorities for today:
1. [Most urgent Slack item or Jira ticket]
2. [Second priority — Jira or Slack]
3. [One thing to keep an eye on]

Have a great day! 💪
```
Derive the top 3 from the actual results — pick the highest-priority Slack mention and Jira tickets. Do not make up items.

Priority rules for the “Today’s Focus” top 3:
- Slack: prioritize `🔴 DIRECT MENTIONS (Action needed)` first; if none exist, use `CHANNEL & THREAD ACTIVITY` items marked `👉 Action needed`.
- Jira: prioritize groups in this order: `🔴 BLOCKED` → `🔵 WAITING FOR YOUR ACTION` → `🟡 IN PROGRESS` → `🟢 TO DO / BACKLOG`.
- Uniqueness: do not repeat the same Slack message or the same Jira ticket twice in the top 3.
- If fewer than 3 eligible items exist, use the best available items; if nothing exists at all, print an honest fallback like “No actionable Slack mentions or Jira tickets found today.”

## Output format
If `Agent` is available, sections may appear in the order they finish (not necessarily Slack → Jira → News → Standup).
If `Agent` is NOT available, sections appear in order: Slack → Jira → News (Mondays only) → Standup → Focus.
Each section is separated by its header line (━━━ emoji TITLE ━━━).

## Error handling
- If a subagent fails or its MCP is disconnected: show an error banner for that section and continue
  ```
  ━━━ 📬 SLACK ━━━
  ⚠️  Slack is not connected. Skipping this section.
  ```
- If all fail: "All tools are currently disconnected. Please check your MCP settings in Claude Desktop."
- Never stop early — always attempt all sections even if one fails
