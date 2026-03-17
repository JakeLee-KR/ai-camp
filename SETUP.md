# Swingvy AI Camp — Pre-Camp Setup Guide

Complete these steps **before Day 1** of the AI Camp. If you get stuck, ask in **#claude-code** on Slack.

---

## Step 1: Install Git

Git is a tool that lets you download and sync the camp materials.

### Check if you already have it

Open **Terminal** (Mac: press `Cmd + Space`, type "Terminal", press Enter) and type:

```bash
git --version
```

- If you see a version number (e.g., `git version 2.x.x`) — skip to Step 2.
- If you see "command not found" or a popup asking to install — follow below.

### Mac

A popup may appear saying *"The 'git' command requires the command line developer tools."* — click **Install** and wait for it to finish.

If no popup appears, run this in Terminal:

```bash
xcode-select --install
```

After installation, verify: `git --version`

### Windows

1. Go to https://git-scm.com/download/win
2. Download and run the installer
3. Use all default settings (just keep clicking Next)
4. After installation, open **Command Prompt** and verify: `git --version`

---

## Step 2: Install Claude Desktop App

1. Go to **https://claude.ai/download**
2. Download the installer for your OS (Mac or Windows)
3. Run the installer and follow the on-screen prompts
4. Launch the **Claude Desktop App** from Applications (Mac) or Start Menu (Windows)
5. Sign in with your Anthropic account

---

## Step 3: Install Claude Code (CLI)

Claude Code is the command-line version of Claude. Even though you'll mainly use the Desktop App, we need the CLI installed because Day 2's tool connections (Slack, Jira, Google, etc.) require terminal commands.

### Mac

Open **Terminal** and run:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

After installation, verify:

```bash
claude --version
```

You should see a version number like `2.x.x`.

### Windows

Open **Command Prompt** and run:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

After installation, verify:

```bash
claude --version
```

> If `curl` is not available on Windows, download and install from https://claude.ai/install

---

## Step 4: Clone the AI Camp Repository

This downloads all the camp materials to your computer.

Open **Terminal** and run these commands one by one:

```bash
# Go to your Desktop (so it's easy to find)
cd ~/Desktop

# Download the camp materials
git clone https://github.com/Swingvy/ai-camp.git

# Go into the camp folder
cd ai-camp
```

You should now have an `ai-camp` folder on your Desktop.

---

## Step 5: Verify Everything Works

Run these checks in Terminal:

```bash
# Check Git
git --version

# Check Claude Code CLI
claude --version

# Check you're in the camp folder
pwd
# Should show something like: /Users/yourname/Desktop/ai-camp

# Check the files are there
ls
# Should show: CLAUDE.md, PROGRAM.md, README.md, SETUP.md
```

---

## Setup Checklist

Before Day 1, confirm you have:

- [ ] **Git** installed (`git --version` shows a version number)
- [ ] **Claude Desktop App** installed and signed in
- [ ] **Claude Code CLI** installed (`claude --version` shows a version number)
- [ ] **ai-camp** repo cloned to your Desktop
- [ ] You can see `CLAUDE.md` and `PROGRAM.md` when you run `ls` in the ai-camp folder

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| `git: command not found` (Mac) | Run `xcode-select --install` in Terminal |
| `git: command not found` (Windows) | Download from https://git-scm.com/download/win |
| `claude: command not found` | Run the install command from Step 3 again |
| "Permission denied" when cloning | Ask IT to check your GitHub access to Swingvy/ai-camp |
| Claude Desktop App won't open | Re-download from https://claude.ai/download |
| "Repository not found" | Make sure the URL is exactly `https://github.com/Swingvy/ai-camp.git` |

---

Need help? Post in **#claude-code** on Slack or ask your camp instructor.
