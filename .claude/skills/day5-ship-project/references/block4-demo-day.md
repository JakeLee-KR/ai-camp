# Block 4: Demo Day & Submit

## EXPLAIN

This is the moment. Everyone demos, everyone celebrates, everyone submits.

### Demo Order

The instructor will set the order. Each person gets 3 minutes:
- 30 sec: Problem
- 90 sec: Live demo
- 30 sec: Impact
- 30 sec: What's next

After all demos: vote for "Most Impactful" and "Most Creative"

### Submitting Your Project

After demos, submit your project to the demo day repository via Pull Request.

**What to submit:**
```
your-github-id/
├── PRD.md           (your project document)
└── skills/
    ├── main-skill/
    │   └── SKILL.md
    └── helper-skill/  (if you have one)
        └── SKILL.md
```

### Git Guide — Step by Step

Follow these steps in **Terminal** to submit your project. If you get stuck at any step, ask Claude for help.

#### Step 1: Clone the Demo Day Repository

This downloads the demo day repo to your computer (only needed once):

```bash
# Go to your Desktop
cd ~/Desktop

# Clone the demo day repo
gh repo clone Swingvy/ai-camp-demo-day

# Go into it
cd ai-camp-demo-day
```

> **Already cloned it?** Just go to the folder and get the latest:
> ```bash
> cd ~/Desktop/ai-camp-demo-day
> git checkout main
> git pull origin main
> ```

#### Step 2: Create Your Branch

Each person submits on their own branch. Use your GitHub username:

```bash
# Create your branch
git checkout -b project/your-github-id
```

Replace `your-github-id` with your actual GitHub username (e.g., `project/jin-kim`).

#### Step 3: Create Your Project Folder

```bash
# Create your folder
mkdir -p your-github-id/skills
```

#### Step 4: Upload Your Project Files

Copy your PRD and skill files into your folder. Ask Claude for help:

```
Help me copy my project files to the demo day repo.
My PRD is at [location].
My skills are in .claude/skills/[skill-name]/.
My folder in the repo is: your-github-id/
```

Or manually copy:
```bash
# Copy your PRD
cp /path/to/your/PRD.md your-github-id/PRD.md

# Copy your skill(s)
cp -r /path/to/your/.claude/skills/your-skill your-github-id/skills/
```

#### Step 5: Commit and Push

```bash
# Stage all your files
git add your-github-id/

# Commit with a message
git commit -m "feat: your-github-id final project submission"

# Push your branch to GitHub
git push origin project/your-github-id
```

#### Step 6: Create a Pull Request

```bash
gh pr create --title "Project: your-github-id" --body "## Project: [Your Project Title]

- Skills: /skill-1, /skill-2
- Impact: [before] → [after]
- PRD: included"
```

#### Quick Reference — The Full Flow

```
cd ~/Desktop/ai-camp-demo-day          ← Go to the repo
git checkout main && git pull           ← Get latest
git checkout -b project/your-id         ← Create your branch
mkdir -p your-id/skills                 ← Create your folder
                                        ← (copy your files in)
git add your-id/                        ← Stage your files
git commit -m "feat: your-id project"   ← Save with a note
git push origin project/your-id         ← Upload to GitHub
gh pr create --title "Project: your-id" ← Create PR for review
```

#### Troubleshooting

| Problem | Solution |
|---------|----------|
| `gh` not found | Install GitHub CLI: `brew install gh` (Mac) |
| Not logged in | Run `gh auth login` and follow the prompts |
| "Permission denied" | Ask your instructor to add you to the Swingvy/ai-camp-demo-day repo |
| "Branch already exists" | Use a different name: `project/your-id-v2` |
| Forgot to pull latest | `git checkout main && git pull origin main`, then create your branch again |

## EXECUTE

### During demos:
- When it's your turn, present your 3-minute demo
- When others present, take notes on skills that could help YOUR work
- Vote for "Most Impactful" and "Most Creative"

### After demos, submit your project:

Follow the Git Guide above step by step, or ask Claude:
```
Help me submit my project to the ai-camp-demo-day repository.
My GitHub ID is [your-id].
Walk me through each git step.
My project files are in [location].
```

Claude will guide you through cloning, branching, adding files, committing, pushing, and creating the PR.

### Camp Completion

After successful submission, you've completed the camp!

```
=== Camp Complete ===

You have:
✅ Installed Claude Code
✅ Mastered GUI vs CLI basics
✅ Created your CLAUDE.md profile
✅ Connected your work tools via Connectors
✅ Built custom skills
✅ Created multi-skill workflows
✅ Shipped a real project
✅ Submitted to the team repository

What's next:
→ Use your skills daily at work
→ Build new skills when you spot repetitive tasks
→ Help a colleague get started with Claude Code
→ Contribute improvements to the team skills repo
→ Join #ai-camp on Slack for tips and support
```

## QUIZ

Final quiz — a reflection:

```
AskUserQuestion({
  "questions": [{
    "question": "What will you do FIRST on Monday morning with Claude Code?",
    "header": "Looking Forward",
    "options": [
      {"label": "Run my new skill on real work data", "description": ""},
      {"label": "Show a colleague what I built", "description": ""},
      {"label": "Build another skill for a different task", "description": ""},
      {"label": "All of the above!", "description": ""}
    ],
    "multiSelect": false
  }]
})
```

All answers are correct! The point is that you're already thinking about using Claude Code in your real work. That means the camp worked.

End with:
```
The camp is over, but this is just the beginning.
You now have a skill that most people don't — you can build with AI.
Every repetitive task you spot is an opportunity for a new skill.
Every tool you use is a candidate for connection.
Every workflow is a potential automation.

Welcome to the team that builds with AI.
```
