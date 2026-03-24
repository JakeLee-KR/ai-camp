---
name: daily-news
description: "Greet the user with today's date and surface 5 top news items about AI agents being used for software testing — tools, frameworks, case studies, and announcements."
---

# Daily News: AI Agents for Software Testing

## INPUT
- Today's date (from system)
- Live web search results about AI agents used in software testing

## PROCESS

**Step 1: Greet the user**
Print a friendly greeting with today's date:
```
Good morning! Today is [Day], [Month DD YYYY].
Here's your daily digest: AI Agents for Software Testing ☕
```

**Step 2: Search for news**
Run these 3 searches in parallel using the WebSearch tool:
1. `AI agent software testing automation [current year]`
2. `autonomous QA agent test generation self-healing tests`
3. `AI agent QA engineer testing tool announcement site:techcrunch.com OR site:thenewstack.io OR site:twitter.com`

Focus only on news about **AI agents used in software testing**, including:
- AI agents that write, run, or fix tests autonomously
- Self-healing test frameworks
- Tools or vendors adding agentic QA capabilities
- Case studies of AI agents augmenting or replacing QA engineers

**Step 3: Pick the 5 best results**
Select the 5 most recent and relevant items across all searches.
Prefer results from the last 24–48 hours when available.

**Step 4: Format the digest**
Present each item as:
```
[N]. 📰 [HEADLINE]
   Source: [source name · date]
   Summary: [1–2 sentence plain-language summary]
   Link: [URL]
```

**Step 5: Close with a takeaway**
Add one closing line:
```
💡 Today's takeaway: [one sentence connecting a theme across the 5 items]
```

## OUTPUT
A scannable 5-item digest of today's most relevant news on AI agents for software testing, with sources, summaries, links, and a closing insight.

## RULES
- Always fetch live results — never make up or hallucinate news
- If fewer than 5 fresh results exist, use the best available and note the date
- Keep summaries short — no walls of text
- If a source is Twitter/X or Threads, label it clearly
