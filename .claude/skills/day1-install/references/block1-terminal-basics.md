# Block 1: GUI vs CLI — Two Ways to Talk to Your Computer

## EXPLAIN

There are two ways to interact with your computer:

**GUI (Graphical User Interface)** — what you're used to
- Clicking icons, dragging files, using menus
- Examples: Finder, Chrome, Slack, Microsoft Word
- Visual, intuitive, point-and-click

**CLI (Command Line Interface)** — what developers use
- Typing text commands in a terminal window
- Examples: Terminal (Mac), Command Prompt (Windows)
- Fast, powerful, automatable

### Why does this matter?

Claude Code works through a **CLI-style interface** inside the Claude Desktop App. Instead of clicking buttons, you type natural language instructions. Understanding the CLI concept will help you feel comfortable.

### The Terminal — Your First CLI

The terminal is just a text-based way to talk to your computer. Instead of clicking icons, you type commands. That's it.

### The 6 Commands You Need

| What you want | Command | What it does |
|---------------|---------|-------------|
| "Where am I?" | `pwd` | Shows your current folder path |
| "What's in here?" | `ls` | Lists files and folders |
| "Go into a folder" | `cd folder-name` | Opens/enters a folder |
| "Go back up" | `cd ..` | Goes to the parent folder |
| "Make a folder" | `mkdir my-folder` | Creates a new folder |
| "Clean the screen" | `clear` | Clears all the text |

### How to open the terminal

**Mac:**
- Spotlight (Cmd + Space) → type "Terminal" → Enter
- Or: Applications → Utilities → Terminal

**Windows:**
- Search → "Command Prompt" or "PowerShell" → Enter

### Reading the terminal

```
Jin@MacBook ~ %
```

This is the **prompt**. It shows:
- `Jin` = your username
- `MacBook` = your computer name
- `~` = you're in your home folder
- `%` = ready for your command

You type after the `%` and press Enter.

## EXECUTE

Let's experience the CLI! Open your terminal and try these commands in order:

```bash
# 1. Where am I?
pwd

# 2. What's in here?
ls

# 3. Make a camp folder
mkdir claude-camp

# 4. Go into it
cd claude-camp

# 5. Confirm you're there
pwd

# 6. Go back
cd ..

# 7. Clean up
clear
```

Try each one and see what happens. Don't worry — these commands are completely safe. They just look around and create a folder.

## QUIZ

```
AskUserQuestion({
  "questions": [
    {
      "question": "What is the difference between GUI and CLI?",
      "header": "GUI vs CLI",
      "options": [
        {"label": "GUI uses visual elements (icons, menus, clicks); CLI uses text commands", "description": ""},
        {"label": "GUI is for Macs, CLI is for Windows", "description": ""},
        {"label": "GUI is newer, CLI is outdated", "description": ""},
        {"label": "There is no difference", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "What do these commands stand for? Match: pwd, ls, mkdir, cd",
      "header": "Commands",
      "options": [
        {"label": "pwd = Print Working Directory, ls = List, mkdir = Make Directory, cd = Change Directory", "description": ""},
        {"label": "pwd = Password, ls = List System, mkdir = Make Dir, cd = Copy Data", "description": ""},
        {"label": "pwd = Path of Working Dir, ls = Load System, mkdir = Move Directory, cd = Close Directory", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})
```

**Question 1** — Correct answer: "GUI uses visual elements (icons, menus, clicks); CLI uses text commands"

If correct: "Exactly! GUI = Graphical (clicking icons), CLI = Command Line (typing commands). Claude Code uses a CLI-style interface where you type instructions in natural language. You'll get comfortable with it quickly!"
If incorrect: "GUI (Graphical User Interface) is the visual, click-based way you normally use your computer — icons, menus, windows. CLI (Command Line Interface) is text-based — you type commands instead of clicking. Claude Code works through a CLI-style interface, but don't worry — you'll type in plain English, not technical commands."

**Question 2** — Correct answer: "pwd = Print Working Directory, ls = List, mkdir = Make Directory, cd = Change Directory"

If correct: "Nice! Now you know what you're actually telling your computer. `pwd` prints where you are, `ls` lists what's there, `mkdir` makes a new directory (folder), and `cd` changes which directory you're in. And `cd ..` just means 'change directory to the parent folder' — the `..` always means 'one level up'."
If incorrect: "Here's what they stand for: `pwd` = **P**rint **W**orking **D**irectory (show where I am), `ls` = **L**i**s**t (show what's here), `mkdir` = **M**a**k**e **Dir**ectory (create a folder), `cd` = **C**hange **D**irectory (go to a folder). And `cd ..` means 'go up one level' — `..` always refers to the parent folder."
