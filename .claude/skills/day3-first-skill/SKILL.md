---
name: day3-first-skill
description: "Internal Camp Day 3: Build your first Claude Code Skill. Covers skill discovery (skills.sh), skill anatomy, writing SKILL.md with Custom Skill Builder, testing, and iteration. Use for \"Day 3\", \"first skill\", \"build skill\", \"make skill\", \"SKILL.md\"."
---

# Day 3: Build Your First Skill

This skill guides participants through creating their first reusable Claude Code Skill — from discovering existing skills on skills.sh, to understanding skill anatomy, to writing, testing, and refining a working SKILL.md using the Custom Skill Builder.

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
| 0 | `references/block0-what-is-skill.md` | What is a Skill? + Discover skills on skills.sh |
| 1 | `references/block1-find-your-task.md` | Identify your repetitive task |
| 2 | `references/block2-skill-anatomy.md` | Anatomy of SKILL.md + official skill-creator |
| 3 | `references/block3-write-skill.md` | Write your skill with Custom Skill Builder |
| 4 | `references/block4-test-iterate.md` | Test, break, fix, improve |
| 5 | `references/block5-share.md` | Demo to the group |

---

## Role-specific Skill Ideas

When helping participants in Block 1, suggest relevant ideas based on their role:

| Role | Skill idea | What it does |
|------|-----------|--------------|
| HR | `/onboarding-checklist` | Generate personalized onboarding docs for new hires |
| Finance | `/expense-summary` | Summarize expense reports from shared drive |
| Marketing | `/social-draft` | Draft social media posts from product updates |
| Sales | `/deal-brief` | Compile customer info before a sales call |
| CS | `/ticket-summary` | Summarize support tickets by category |
| Ops | `/vendor-compare` | Compare vendor proposals side by side |
| PM | `/sprint-recap` | Generate sprint recap from project management tool |
| Legal | `/contract-review` | Extract key terms from contract drafts |

---

## Skill Template

When participants reach Block 3, guide them to use the Custom Skill Builder:
- Install: https://github.com/Swingvy/skill-to-build-skill
- The builder will interactively help create a well-structured SKILL.md

---

## Interaction Rules

- Help participants think in terms of INPUTS → PROCESS → OUTPUT
- Encourage starting small (1 simple task) rather than building something complex
- Emphasize: "A skill is just instructions in plain language, not code"
- When testing skills, help debug by reading the SKILL.md and suggesting improvements
- Celebrate every working skill, no matter how simple
- Language: English

---

## Start

```
AskUserQuestion({
  "questions": [{
    "question": "Where would you like to start?",
    "header": "Day 3: Build Your First Skill",
    "options": [
      {"label": "Block 0: What is a Skill?", "description": "See a skill in action + discover existing skills"},
      {"label": "Block 1: Find Your Task", "description": "Identify the repetitive task you'll automate"},
      {"label": "Block 2: Skill Anatomy", "description": "Learn the structure of SKILL.md"},
      {"label": "Block 3: Write Your Skill", "description": "Create your skill with Custom Skill Builder"},
      {"label": "Block 4: Test & Iterate", "description": "Run it, break it, fix it, improve it"},
      {"label": "Block 5: Share", "description": "Demo your skill to the group"}
    ],
    "multiSelect": false
  }]
})
```
