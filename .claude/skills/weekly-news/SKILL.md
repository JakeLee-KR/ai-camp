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

**When running inside `/morning-valet`:** If the prefs file exists and contains `industry`, `department`, and `last_topic`, use all three values silently — skip Steps 2–4 entirely and jump straight to Step 5. If the file exists but `last_topic` is missing, auto-generate a topic label from industry × department (no web search): take the first base topic for that department and lightly combine it with the industry keyword, then save it — still no questions asked. If the file does not exist, use defaults silently (`industry: "HR Tech / SaaS"`, `department: "QA"`) and auto-generate a topic, then save:
```json
{ "industry": "HR Tech / SaaS", "department": "QA", "last_topic": "[auto-generated]", "setup_complete": true }
```

**When running standalone:**

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

Then save the chosen values to `~/.claude/weekly-news-prefs.json` (preserve any existing fields like `last_topic` and `setup_complete`):
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

After the user picks, save the choice to `~/.claude/weekly-news-prefs.json` as `"last_topic": "[chosen topic]"`. Preserve all existing fields. On subsequent runs (when `last_topic` exists), skip the topic picker and use the saved topic directly. The user can say "change my news topic" to re-pick.

**Step 5: Greet the user**
Print a friendly greeting with today's date and their chosen topic:
```
Good morning! Today is [Day], [Month DD YYYY].
Here's your weekly digest: [TOPIC] ☕
```

**Step 6: Search for news**
Calculate:
- `[30-days-ago date]` (e.g. 2026-03-26 -> 2026-02-24)
- `[7-days-ago date]` for later “this week” checks
Run these 4 searches in parallel using the WebSearch tool, using `after:[30-days-ago date]`:
1. `[TOPIC] news after:[30-days-ago date]`
2. `[TOPIC] announcement release after:[30-days-ago date]`
3. `[TOPIC] tool update case study [current year]`
4. `[TOPIC] site:twitter.com OR site:x.com OR site:threads.net after:[30-days-ago date]`

**Step 7: Pick the 5 most recent results**
Sort all results from the 4 searches by publish date (newest first). Take the top 5.

- Let `[count_7d]` be how many of the *selected top 5* are from the past 7 days (publish date >= `[7-days-ago date]`).
- **If `[count_7d] >= 3`:** Show them — no extra message needed.
- **If `[count_7d] < 3`:** Show this message before the digest:
  ```
  📭 Not much happened in [TOPIC] this week. Here are the most recent items from the past 30 days:
  ```
- **If no meaningful results at all (0–1 results total):** Skip the digest and say:
  ```
  📭 Nothing special this week in [TOPIC]. Check back next week!
  ```
  Then end the skill without sending a Slack DM.

Ensure at least 1 item is from X or Threads if available:
If the top 5 contains 0 X/Threads items but there are X/Threads results within the overall result set, replace the least-recent non-X/Threads item in the top 5 with the most recent X/Threads item.

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
- Prefer items from the last 7 days; note the date if older (but you may include up to ~30 days back when the week was slow)
- Keep summaries short — no walls of text
- Label X (Twitter) posts as `🐦 X (Twitter)` and Threads posts as `🧵 Threads`
- Prioritise at least 1 result from X or Threads if available
- Always look up the current user's Slack ID dynamically — never hardcode a user ID
- Send the digest as a Slack DM to whoever is running the skill

## Error handling
- If WebSearch fails or returns an empty set: treat it like “0 meaningful results” and skip the DM.
- If Slack MCP is not connected: print the digest to the terminal, but do NOT attempt the DM; instead tell the user to copy-paste.
- If Slack ID lookup fails: print the digest to the terminal and tell the user the DM step was skipped (lookup failed).
