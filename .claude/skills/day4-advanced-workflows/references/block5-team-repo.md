# Block 5: Team Skills Repository

## EXPLAIN

Your skills are valuable not just to you, but to everyone in your role. A **team skills repository** is a shared collection of skills that the whole team can use.

### The Concept

```
Today:
  HR-Jin has /onboarding-pack
  HR-Mina has /interview-summary
  Marketing-Alex has /social-draft

  → Each person has their own skills, nobody else benefits

After team repo:
  Shared repo has ALL skills
  → Everyone can use everyone's skills
  → New hires get instant access to all team automation
```

### How It Works

1. **Create a shared GitHub repo** (e.g., `company/team-skills`)
2. **Each person contributes** their skills via Pull Request
3. **Everyone clones** the repo and gets all skills
4. **Skills improve** over time as people submit updates

### Repository Structure

```
team-skills/
├── CLAUDE.md           (team-wide settings)
├── .claude/
│   └── skills/
│       ├── hr/
│       │   ├── onboarding-pack/SKILL.md
│       │   └── interview-summary/SKILL.md
│       ├── marketing/
│       │   ├── social-draft/SKILL.md
│       │   └── campaign-report/SKILL.md
│       ├── sales/
│       │   ├── deal-brief/SKILL.md
│       │   └── prospect-research/SKILL.md
│       └── shared/
│           ├── meeting-prep/SKILL.md
│           └── weekly-report/SKILL.md
```

### Step 0: Sign Up for a GitHub Account

Before using the team repo, you need a **GitHub account**. If you already have one, skip to the next section.

1. Go to **https://github.com/signup**
2. Enter your **work email address**
3. Create a **password** and choose a **username**
4. Complete the verification steps
5. Once signed up, let your instructor know your GitHub username so they can add you to the team repo

> **Already have an account?** Make sure you're logged in at github.com before continuing.

### Git for Non-Engineers (Step by Step)

**First time setup:**
```bash
# Download the team repo
gh repo clone company/team-skills

# Go into it
cd team-skills
```

**Contributing your skill:**
```bash
# Get latest version
git pull

# Create your own workspace
git checkout -b add/my-skill-name

# Copy your skill into the right folder
# (Claude can help with this)

# Save your changes
git add .
git commit -m "Add my-skill-name skill"

# Upload to GitHub
git push origin add/my-skill-name

# Create a review request
gh pr create --title "Add my-skill-name" --body "This skill does X for Y role"
```

Don't worry if this feels complex — Claude can walk you through each step interactively.

### Getting Other People's Skills

```bash
# Pull the latest skills from the team repo
cd team-skills
git pull

# All skills are now available
# Type /skill-name to use any of them
```

## EXECUTE

Let's practice the git workflow:

1. If your instructor has set up a team repo, clone it:
```
Ask Claude: "Help me clone the team-skills repo and add my skill to it.
Walk me through each step."
```

2. If no team repo exists yet, practice the git flow with a personal repo:
```
Ask Claude: "Help me create a GitHub repository called 'my-skills',
push my skills from .claude/skills/ to it, and create a README."
```

3. Either way, the goal is to practice:
   - `git add` (stage your changes)
   - `git commit` (save with a message)
   - `git push` (upload to GitHub)
   - `gh pr create` (request a review)

Claude will guide you through each command. Ask questions if anything is unclear.

## QUIZ

```
AskUserQuestion({
  "questions": [{
    "question": "What is the main benefit of a team skills repository?",
    "header": "Team Repo Quiz",
    "options": [
      {"label": "It makes skills run faster", "description": ""},
      {"label": "Everyone can use everyone's skills — automation compounds across the team", "description": ""},
      {"label": "It's required by GitHub", "description": ""},
      {"label": "It replaces CLAUDE.md", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

Correct answer: "Everyone can use everyone's skills — automation compounds across the team"

If correct: "Yes! One person's skill becomes the whole team's tool. If 5 people each build 2 skills, the team has 10 skills. New hires get all 10 on day one. Automation compounds — that's the power of sharing."
If incorrect: "The real power is compounding. When everyone shares skills, each person benefits from everyone else's work. If 10 people build 2 skills each, the team has 20 automated workflows. A new hire gets all 20 immediately. That's how teams scale with AI."
