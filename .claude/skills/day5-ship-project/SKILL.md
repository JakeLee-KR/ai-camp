---
name: day5-ship-project
description: "Internal Camp Day 5: Ship your project. Build a complete solution, write a PRD, demo to the group, and submit via PR. Use for \"Day 5\", \"ship\", \"project\", \"demo day\", \"final project\"."
---

# Day 5: Ship Your Project

## 🎯 The Goal

> **Ship a real project and demo it to the team.**
>
> By the end of today, you'll have built a complete solution that solves a real problem from your job, written a PRD, presented a live demo, and submitted your project to the team repository.

---

## Flow Overview

```
Block 0          Block 1           Block 2          Block 3          Block 4
Plan your   →   Build it      →   Write PRD   →   Demo prep    →   Demo Day
project          (guided sprint)    & validate       & rehearse       & submit
```

This day is less lecture, more building. The skill acts as a coach throughout.

---

## Block Map

| Block | File | Topic | Time |
|-------|------|-------|------|
| 0 | `references/block0-plan.md` | Define your project | ~20 min |
| 1 | `references/block1-build.md` | Guided build sprint | ~90 min |
| 2 | `references/block2-prd.md` | Write & validate PRD | ~20 min |
| 3 | `references/block3-demo-prep.md` | Prepare your demo | ~15 min |
| 4 | `references/block4-demo-day.md` | Demo Day + submit PR | ~30 min |

---

## Project Requirements

Every project must include:

| Requirement | What it means |
|-------------|---------------|
| Real problem | Solves something from your actual daily work |
| MCP connection | Uses at least 1 external tool (Slack, Notion, etc.) |
| Custom skill | Has at least 1 working SKILL.md |
| PRD document | Problem, solution, skills table, how to use |
| Live demo | Can show it working in 2 minutes |

---

## Project Ideas by Role

| Role | Project | Skills involved |
|------|---------|----------------|
| HR | Onboarding automation | `/generate-onboarding-pack` + `/first-week-checklist` |
| Finance | Expense reporting pipeline | `/pull-expenses` + `/expense-report` |
| Marketing | Content pipeline | `/draft-social` + `/review-tone` + `/schedule-post` |
| Sales | Deal preparation system | `/research-prospect` + `/deal-brief` + `/meeting-agenda` |
| CS | Ticket triage system | `/categorize-tickets` + `/draft-responses` |
| Ops | Vendor management | `/compare-vendors` + `/vendor-scorecard` |
| PM | Sprint management | `/collect-updates` + `/sprint-report` + `/blockers-alert` |
| Legal | Contract analysis | `/extract-terms` + `/risk-checklist` |

---

## PRD Template

```markdown
# [Project Title]

## Problem
> One line: whose problem, what problem, how you solve it

- **Current state**: (specific numbers — how many, how long, how often)
- **Desired state**: (what it looks like when working)
- **Success criteria**: (1-2 measurable outcomes)

## Skills

| # | Skill name | Description | Status |
|---|-----------|-------------|--------|
| 1 | `/my-skill-1` | input → output | Working / In progress |
| 2 | `/my-skill-2` | input → output | Working / In progress |

## MCP Connections Used
- Tool 1: what data it provides
- Tool 2: what data it provides

## How to Use
1. Step 1
2. Step 2
3. Step 3

## Impact
- Before: (time/effort required)
- After: (time/effort with this solution)
```

---

## PRD Validation Checklist

When validating a PRD in Block 2, check:

| # | Item | Check |
|---|------|-------|
| 1 | Project title | `#` heading exists |
| 2 | Problem section | `## Problem` exists |
| 3 | Current state | Present and 10+ characters |
| 4 | Desired state | Present and 10+ characters |
| 5 | Success criteria | Present and 10+ characters |
| 6 | Skills section | `## Skills` exists |
| 7 | At least 1 skill | Skills table has 1+ data rows |
| 8 | MCP section | `## MCP Connections Used` exists |
| 9 | How to use | `## How to Use` exists |

Output format:
```
=== PRD Validation ===
✅ Project title: found
✅ Problem section: found
...
Result: 9/9 PASS
```

If any fail, explain what's missing and help fix it.

---

## Demo Format (Block 4)

Guide each participant to prepare a 3-minute demo:

```
[0:00 - 0:30]  Problem: "Every week I spend 2 hours doing X..."
[0:30 - 2:00]  Live demo: Run the skill, show the output
[2:00 - 2:30]  Impact: "Now it takes 5 minutes instead of 2 hours"
[2:30 - 3:00]  What's next: "I plan to add Y and Z"
```

---

## Submission (PR)

After demo, guide the PR submission to **https://github.com/Swingvy/ai-camp-demo-day**:

1. Clone repo: `gh repo clone Swingvy/ai-camp-demo-day`
2. Create branch: `git checkout -b project/{github-id}`
3. Create folder: `mkdir -p {github-id}/skills`
4. Copy files: PRD.md + skill files into `{github-id}/`
5. Commit: `git add {github-id}/ && git commit -m "feat: {github-id} final project"`
6. Push: `git push origin project/{github-id}`
7. Create PR: `gh pr create --title "Project: {github-id}"`

Block 4 reference file has the full step-by-step Git guide for non-engineers.

---

## Interaction Rules

- Block 0: Help narrow scope — "What's the smallest version that works?"
- Block 1: Act as a build coach — unblock issues, suggest approaches, keep momentum
- Block 2: Be strict on PRD validation — quality matters
- Block 3: Help rehearse — "Can you explain the problem in one sentence?"
- Block 4: Celebrate everything — every project shipped is a win
- Throughout: remind participants they're building something REAL for their ACTUAL job

---

## Completion Report

After successful submission:

```
=== Camp Complete ===

Participant: {name}
Project: {title}
Skills built: {count}
MCP connections: {list}
PRD: PASS ({n}/9)
PR: {url}

🎉 You shipped a real project using Claude Code.
   You are now part of the team that builds with AI.

Next steps:
- Use your skills daily
- Add new skills as you find new repetitive tasks
- Help a colleague get started
- Share improvements in #ai-camp
```

---

## Start

```
AskUserQuestion({
  "questions": [{
    "question": "Where would you like to start?",
    "header": "Day 5: Ship Your Project",
    "options": [
      {"label": "Block 0: Plan", "description": "Define your project scope and requirements"},
      {"label": "Block 1: Build", "description": "Guided sprint — build your solution"},
      {"label": "Block 2: PRD", "description": "Write and validate your project document"},
      {"label": "Block 3: Demo Prep", "description": "Prepare your 3-minute presentation"},
      {"label": "Block 4: Demo Day", "description": "Present + submit via PR"}
    ],
    "multiSelect": false
  }]
})
```
