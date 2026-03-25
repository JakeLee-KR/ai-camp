# Block 5: Team Skills Repository

## EXPLAIN

Your skills are valuable not just to you, but to everyone in your role. A **team skills repository** is a shared collection of skills that the whole team can use.

### The Problem

```
Today:
  HR-Jin has /onboarding-pack
  HR-Mina has /interview-summary
  Marketing-Alex has /social-draft

  → Each person has their own skills, nobody else benefits
```

### The Solution

```
After team repo:
  Shared repo has ALL skills
  → Everyone can use everyone's skills
  → New hires get instant access to all team automation
```

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

### Step 1: Install GitHub CLI

GitHub CLI (`gh`) makes it easy to work with GitHub from your Terminal. Install it now:

**Mac:**
```bash
brew install gh
```

> If `brew` is not found, install Homebrew first:
> ```bash
> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
> ```

**Windows:**
```bash
winget install --id GitHub.cli
```

**Verify and log in:**
```bash
# Check it's installed
gh --version

# Log in to GitHub
gh auth login
```

When running `gh auth login`, select:
- **GitHub.com**
- **HTTPS**
- **Login with a web browser** → copy the code, open the URL, paste the code

### Git 101 Summary

Here are the essential Git commands you'll use. Think of Git as a "save and share" system for your files:

| Command | What it does | Plain English |
|---------|-------------|---------------|
| `git pull` | Download the latest changes | "Get the newest version" |
| `git checkout -b branch-name` | Create your own workspace | "Make a copy to work in" |
| `git add .` | Select files to save | "Pick what to include" |
| `git commit -m "message"` | Save with a description | "Save my work with a note" |
| `git push` | Upload to GitHub | "Share my work online" |
| `gh pr create` | Request a review | "Ask the team to review" |

**The full flow:**
```
git pull                              ← Get latest
git checkout -b add/my-skill          ← Create your workspace
                                      ← (make your changes)
git add .                             ← Select changes
git commit -m "Add my-skill"          ← Save with a note
git push origin add/my-skill          ← Upload to GitHub
gh pr create --title "Add my-skill"   ← Ask for review
```

## EXECUTE

Let's practice the git workflow with a personal repo.

Ask Claude:
```
Help me create a GitHub repository called 'my-skills',
push my skills from .claude/skills/ to it, and create a README.
Walk me through each step.
```

This lets you practice the full flow:
- `git pull` → `git checkout -b` → `git add .` → `git commit` → `git push` → `gh pr create`

Claude will guide you through each command. Ask questions if anything is unclear.

---
👆 Try this yourself now.
When you're done, type **"next"** or **"quiz"** to continue.

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
