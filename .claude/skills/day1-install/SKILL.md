---
name: day1-install
description: "Internal Camp Day 1: Install Claude Code & first conversations. Covers GUI vs CLI, Claude Desktop App, CLAUDE.md, web search, and Plan Mode. Use for \"Day 1\", \"install\", \"setup\", \"onboarding\"."
---

# Day 1: Install & First Conversations

This skill teaches non-engineers to understand GUI vs CLI, install the Claude Desktop App, set up CLAUDE.md, and have their first productive conversations including web search and Plan Mode.

---

## STOP PROTOCOL

> This protocol is the top priority rule for this skill.

### Each block runs across exactly 2 turns

```
┌─ Phase A (Turn 1) ─────────────────────────────────────┐
│ 1. Print the BLOCK BANNER (see below)                   │
│ 2. Read the block's reference file (EXPLAIN section)    │
│ 3. Explain the concept in plain, friendly language      │
│ 4. Read the EXECUTE section                             │
│ 5. Say "Try it yourself now" with clear instructions    │
│ 6. STOP HERE. End the turn.                             │
│                                                         │
│ DO NOT: ask questions, run quizzes, call AskUserQuestion│
└─────────────────────────────────────────────────────────┘

  ⬇️ User comes back with "done", "next", "quiz", etc.

┌─ Phase B (Turn 2) ─────────────────────────────────────┐
│ 1. Read the block's QUIZ section                        │
│ 2. Ask the quiz using AskUserQuestion                   │
│ 3. Give feedback (correct/incorrect + explanation)      │
│ 4. Ask if ready for next block via AskUserQuestion      │
│ 5. If yes → next block's Phase A                        │
└─────────────────────────────────────────────────────────┘
```

### Block Banner

At the **very start** of every Phase A, print this banner so the user can easily find where the new block begins:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📘 BLOCK {N}: {BLOCK TITLE}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

This makes it easy to scroll up and find where each block starts.

### Mandatory rules
1. **Phase A: Start with BLOCK BANNER** — always print it first
2. **Phase A: NO AskUserQuestion** — explain + guide → Stop
3. **Phase A: NO quiz** — quiz is Phase B only
4. **Never combine EXPLAIN + QUIZ in one turn**
5. Phase A must end with:
```
---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.
```

---

## Block Map

| Block | File | Topic |
|-------|------|-------|
| 0 | `references/block0-welcome.md` | Welcome + what to expect |
| 1 | `references/block1-terminal-basics.md` | GUI vs CLI introduction |
| 2 | `references/block2-install.md` | Install the Claude Desktop App |
| 3 | `references/block3-first-conversation.md` | First real conversation |
| 4 | `references/block4-claude-md.md` | CLAUDE.md — teach Claude about you |
| 5 | `references/block5-multi-turn.md` | Multi-turn problem solving + web search |
| 6 | `references/block6-plan-mode.md` | Introduction to Plan Mode |

---

## Interaction Rules

- One block at a time
- Navigate with "next", "skip", or block number/name
- For Claude Code questions, use claude-code-guide agent
- Language: English
- Tone: friendly, encouraging, patient — remember these are non-engineers
- Always celebrate small wins ("Great job!", "You just did something most people never try!")

---

## Start

When this skill is invoked, show the block table and ask where to start:

```
AskUserQuestion({
  "questions": [{
    "question": "Where would you like to start?",
    "header": "Day 1: Install & First Conversations",
    "options": [
      {"label": "Block 0: Welcome", "description": "What this camp is about + what you'll build"},
      {"label": "Block 1: GUI vs CLI", "description": "Two ways to talk to your computer"},
      {"label": "Block 2: Install", "description": "Install the Claude Desktop App"},
      {"label": "Block 3: First Conversation", "description": "Talk to Claude for the first time"}
    ],
    "multiSelect": false
  }]
})
```
