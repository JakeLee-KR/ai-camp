---
name: day4-advanced-workflows
description: "Internal Camp Day 4: Advanced skills with multi-skill workflows, chaining, enhancement, and team sharing. Use for \"Day 4\", \"advanced\", \"workflow\", \"chaining\", \"team skills\"."
---

# Day 4: Advanced Skills & Workflows

## 🎯 The Goal

> **Level up your skills with chaining, enhancement, and team sharing.**
>
> By the end of today, you'll have a multi-step workflow (Skill A → Skill B), enhanced with validation and formatting, and shared with the team via a Git repository.

---

## STOP PROTOCOL

> Same 2-turn protocol. Never violate.

```
Phase A: Print BLOCK BANNER → Explain + Execute instructions → STOP
Phase B: Quiz + feedback → next block
```

### Block Banner

At the **very start** of every Phase A, print this banner so the user can easily find where the new block begins:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📘 BLOCK {N}: {BLOCK TITLE}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Phase A must end with:
```
---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.
```

---

## Block Map

| Block | File | Topic |
|-------|------|-------|
| 0 | `references/block0-review-day3.md` | Review: show off your Day 3 skill |
| 1 | `references/block2-chaining.md` | Chaining skills into workflows |
| 2 | `references/block4-enhance-skill.md` | Enhance your skill with techniques |
| 3 | `references/block5-team-repo.md` | Team skills repository + sharing |
| 4 | `references/block4-homework.md` | Homework — prepare for Demo Day |

---

## Key Concepts to Teach

### Chaining
```
/collect-feedback → produces feedback.md
/analyze-feedback → reads feedback.md → produces analysis.md
/draft-response  → reads analysis.md → produces response.md

One command triggers the full pipeline.
```

### Workflow Combinations by Role

| Role | Skill 1 | Skill 2 | Workflow |
|------|---------|---------|----------|
| HR | `/scan-applications` | `/rank-candidates` | Screen → Rank |
| Marketing | `/collect-mentions` | `/draft-report` | Monitor → Report |
| Sales | `/prep-meeting` | `/send-summary` | Research → Brief |
| CS | `/categorize-tickets` | `/auto-response` | Classify → Draft reply |
| PM | `/gather-updates` | `/status-report` | Collect → Summarize |
| Finance | `/pull-transactions` | `/flag-anomalies` | Fetch → Analyze |

---

## Interaction Rules

- Start by having participants show their Day 3 skill (Block 0)
- For chaining: explain as "assembly line — each station does one thing well"
- Focus on practical enhancement of their existing skill, not abstract concepts
- Git workflow for team repo: guide step by step (clone, branch, add, commit, push, PR)
- Language: English

---

## Start

```
AskUserQuestion({
  "questions": [{
    "question": "Where would you like to start?",
    "header": "Day 4: Advanced Skills & Workflows",
    "options": [
      {"label": "Block 0: Review Day 3", "description": "Show your skill + get feedback"},
      {"label": "Block 1: Chaining Skills", "description": "Connect skills into a workflow"},
      {"label": "Block 2: Enhance Your Skill", "description": "Upgrade your existing skill"},
      {"label": "Block 3: Team Repository", "description": "Share skills across the team"}
    ],
    "multiSelect": false
  }]
})
```
