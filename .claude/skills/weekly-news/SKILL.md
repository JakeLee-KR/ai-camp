---
name: weekly-news
description: "Ask the user for their industry and department, then surface 5 personalized news items from the past week. Use for 'weekly news', 'news digest', 'what's new in', 'latest news about'."
---

# Weekly News Digest

## INPUT
- Today's date (from system)
- Industry field (ask the user)
- Department (ask the user)
- Live web search results

## PROCESS

**Step 1: Check for saved preferences**
Check if `~/.claude/weekly-news-prefs.json` exists and is readable.

- **If it exists:** Read the file, load `industry` and `department`, then ask:
  ```
  👋 Welcome back! Last time you chose:
     Industry:   [saved industry]
     Department: [saved department]

  Use the same preferences, or change them?
  ```
  - If "Same" → skip to Step 4 using saved values
  - If "Change" → proceed to Step 2

- **If it does not exist:** Proceed to Step 2 (first-time setup)

**Step 2: Ask for industry field**
Ask the user to select their industry:
- SaaS / B2B Software
- FinTech / Finance
- HealthTech / Healthcare
- E-commerce / Retail
- EdTech / Education
- HR Tech / People Ops
- Logistics / Supply Chain
- Other (let them type their own)

**Step 3: Ask for department**
Ask the user to select their department:
- CEO / Executive
- Sales
- Marketing
- Customer Success (CS)
- Engineering
- Product Management (PM)
- QA

Then save the chosen values to `~/.claude/weekly-news-prefs.json`:
```json
{
  "industry": "[chosen industry]",
  "department": "[chosen department]"
}
```

**Step 4: Suggest topics based on industry + department**
Combine the industry and department to suggest 3 highly relevant news topics.

Use this logic:
- Start with the department's base topics (see below)
- Prefix or filter them with the chosen industry context

**Department base topics:**

| Department | Base Topics |
|---|---|
| CEO / Executive | AI strategy & business trends · Competitor intelligence · AI productivity tools for leaders |
| Sales | AI sales tools & CRM automation · Revenue intelligence · Outreach & pipeline AI |
| Marketing | AI content & copywriting tools · Social media AI · Growth analytics & SEO AI |
| Customer Success | AI support & chatbot tools · Customer feedback automation · CS AI tools & trends |
| Engineering | AI coding assistants · DevOps & CI/CD automation · Developer tools & framework releases |
| Product Management (PM) | AI product management tools · Roadmap & prioritization AI · Product analytics |
| QA | AI agents for software testing · Self-healing test automation · QA tools & framework releases |

**Examples of combined topics:**
- FinTech + QA → "AI agents for FinTech software testing", "Compliance test automation in FinTech", "Self-healing tests for payment systems"
- HealthTech + Engineering → "AI coding tools for HealthTech", "HIPAA-compliant DevOps automation", "HealthTech developer tools 2026"
- SaaS + Marketing → "AI content tools for SaaS marketing", "SaaS growth analytics AI", "Social media AI for SaaS"

Present the 3 combined suggestions as options and let them pick one (or enter their own).

**Step 5: Greet the user**
Print a friendly greeting with today's date and their chosen topic:
```
Good morning! Today is [Day], [Month DD YYYY].
Here's your weekly digest: [TOPIC] ☕
```

**Step 6: Search for news**
Calculate the date 7 days ago (e.g. if today is 2026-03-26, use after:2026-03-19).
Run these 4 searches in parallel using the WebSearch tool:
1. `[TOPIC] news after:[7-days-ago date]`
2. `[TOPIC] announcement release after:[7-days-ago date]`
3. `[TOPIC] tool update case study [current year]`
4. `[TOPIC] site:twitter.com OR site:x.com OR site:threads.net after:[7-days-ago date]`

**Step 7: Pick the 5 most recent results**
Sort all results from the 4 searches by publish date (newest first). Take the top 5.

- **If 3 or more results are from the past 7 days:** Show them — no extra message needed.
- **If fewer than 3 results are from the past 7 days:** Show this message before the digest:
  ```
  📭 Not much happened in [TOPIC] this week. Here are the most recent items from the past 30 days:
  ```
- **If no meaningful results at all (0–1 results total):** Skip the digest and say:
  ```
  📭 Nothing special this week in [TOPIC]. Check back next week!
  ```
  Then end the skill without sending a Slack DM.

Include at least 1 from X or Threads if available.

**Step 8: Format the digest**
Present each item as:
```
[N]. 📰 [HEADLINE]
   Source: [source name · date]
   Summary: [1–2 sentence plain-language summary]
   Link: [URL]
```
Label X posts as `🐦 X (Twitter)` and Threads posts as `🧵 Threads`.

**Step 9: Close with a takeaway**
```
💡 This week's takeaway: [one sentence connecting a theme across the 5 items]
```

**Step 10: Send via Slack DM**
Look up the current user's Slack ID dynamically via the Slack MCP tool (search by name or email), then send the full digest as a DM to that user.

## OUTPUT
A scannable 5-item weekly digest personalized by industry + department, displayed in the terminal AND sent as a Slack DM.

## RULES
- Always fetch live results — never make up or hallucinate news
- Prefer items from the last 7 days; note the date if older
- Keep summaries short — no walls of text
- Label X (Twitter) posts as `🐦 X (Twitter)` and Threads posts as `🧵 Threads`
- Prioritise at least 1 result from X or Threads if available
- Always look up the current user's Slack ID dynamically — never hardcode a user ID
- Send the digest as a Slack DM to whoever is running the skill
