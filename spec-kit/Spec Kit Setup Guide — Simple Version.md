# Spec Kit Setup Guide — New or Existing Repo

Nov 24, 2026 · @Soumyajit

## 1. What you need first

You need just **two things** on your computer. Everything else is extra.

| You need | Why | Check | Get it from |
| --- | --- | --- | --- |
| **Python 3.11 or newer** | Spec Kit runs on Python | `python --version` | [python.org](https://python.org) |
| **pip** | Puts Python tools on your computer | `pip --version` | Comes with Python |

**Nice to have (not required):**

| Tool | Why | Get it |
| --- | --- | --- |
| Git | Lets you undo mistakes by saving snapshots | `winget install --id Git.Git -e` |
| Claude Desktop | The app where you talk to Claude | [claude.ai/download](https://claude.ai/download) |

Already have Python and pip? Skip to step 2.

Before setting up Spec Kit you need **two things** installed on your machine. Everything else is optional.

| Requirement | Why | Check if you have it | Install if missing |
| --- | --- | --- | --- |
| **Python 3.11+** | Spec Kit is a Python tool | `python --version` | [python.org](https://python.org) or `uv python install 3.12` |
| **pip** | Installs Python packages | `pip --version` | Comes with Python |

**Optional but recommended:**

| Tool | Why | Install |
| --- | --- | --- |
| Git | Save snapshots of your code so you can undo mistakes | `winget install --id Git.Git -e` |
| Claude Desktop | The app where you use Spec Kit's slash commands | [claude.ai/download](https://claude.ai/download) |

If you already have Python and pip (most developers do), you can skip straight to step 2.

## 2. Put Spec Kit on your computer (do this once)

Open **Git Bash** or **PowerShell** and type:

```bash
pip install specify-cli
```

Check it worked:

```bash
specify version
```

You should see a number like `1.4.4`. If it says `command not found`, close your terminal, open it again, and try once more.

To update later: `pip install --upgrade specify-cli`

To check if a new version exists: `specify self check`

This installs the `specify` command on your entire computer. You do this **once** — it works across all projects after that.

Open **Git Bash** or **PowerShell** and run:

```bash
pip install specify-cli
```

Verify it installed correctly:

```bash
specify version
```

You should see a version number like `1.4.4`. If you see `command not found`, close your terminal and reopen it, then try again.

**Upgrading later:** when a newer version comes out, run:

```bash
pip install --upgrade specify-cli
```

You can check if an upgrade is available at any time with `specify self check`.

## 3. New project — start from zero

Use this when you have no code yet.

```bash
cd /d/projects                                            # go to where you keep projects
specify init my-app --integration claude                   # makes a new folder called my-app/
cd my-app                                                  # go inside it
```

`--integration claude` tells Spec Kit you use Claude. It creates the `/speckit-...` commands that Claude reads.

If it says "cannot find Claude Code", add `--ignore-agent-tools` at the end. That's safe — the commands still get made.

Use this when you're starting a project from scratch and don't have any code yet.

**Step 1:** Navigate to where you want the project folder created:

```bash
cd /d/projects
```

**Step 2:** Run the init command with a project name:

```bash
specify init my-project-name --integration claude
```

This creates a new folder called `my-project-name/` with the full Spec Kit structure inside it.

**What `--integration claude` does:** It tells Spec Kit that you're using Claude as your AI coding agent. This creates the `.claude/skills/` folder with all the `/speckit-...` slash commands that Claude understands. Without it, Spec Kit wouldn't know which AI you're using.

**Step 3:** Move into the new folder:

```bash
cd my-project-name
```

**Step 4:** If it complains about not finding Claude Code, add `--ignore-agent-tools`:

```bash
specify init my-project-name --integration claude --ignore-agent-tools
```

This skips the check for Claude Code on your system. It's safe — the slash commands still get created.

You're done. Jump to step 5 to pick your script type, then step 6 to verify.

## 4. Existing project — add Spec Kit to code you already have

Use this when your project already has files in it.

```bash
cd /d/dms_fullstack/dms_ui                                      # go to your project
git add . && git commit -m "snapshot before Spec Kit"            # save a backup first (skip if no Git)
specify init --here --force --integration claude                 # add Spec Kit right here
```

What the flags mean:

| Flag | What it does |
| --- | --- |
| `--here` | Use this folder, don't make a new one |
| `--force` | The folder has files already — that's OK |
| `--integration claude` | Make the commands for Claude |

You'll see a warning about the folder not being empty. That's fine. Spec Kit only **adds** its own folders. It does **not** touch your code.

**Already have a `.claude/` folder?** (from code-review-graph or other tools) — no problem. Your old skills stay. Spec Kit puts its own `speckit-*/` folders next to them.

**Already have a `CLAUDE.md`?** It stays. Both files work side by side. Claude reads both.

Use this when you already have a project with code in it and you want to add Spec Kit on top.

**Step 1:** Navigate into your existing project folder:

```bash
cd /d/dms_fullstack/dms_ui
```

**Step 2 (recommended):** If you use Git, save a snapshot first so you can undo if anything goes wrong:

```bash
git add .
git commit -m "chore: snapshot before adding Spec Kit"
```

**Step 3:** Run init with `--here` and `--force`:

```bash
specify init --here --force --integration claude
```

What each flag means:

| Flag | Purpose |
| --- | --- |
| `--here` | Set up Spec Kit in the current folder instead of creating a new one |
| `--force` | The folder already has files in it — that's fine, go ahead |
| `--integration claude` | Create Claude-specific slash commands in `.claude/skills/` |

You'll see a warning: `Current directory is not empty (77 items). Template files will be merged with existing content.` This is normal. Spec Kit only **adds** its own folders (`.specify/`, `.claude/skills/speckit-*/`). It does **not** delete, rename, or change any of your existing files.

**Step 4:** If it says it can't find Claude Code:

```bash
specify init --here --force --integration claude --ignore-agent-tools
```

**What about existing `.claude/` files?** If your project already has a `.claude/` folder (from code-review-graph or other skills), Spec Kit merges into it. Your existing skills like `debug-issue/`, `explore-codebase/`, `refactor-safely/`, `review-changes/` are left untouched. Spec Kit only adds its own `speckit-*/` folders alongside them.

**What about an existing `CLAUDE.md`?** It stays. `CLAUDE.md` and `.specify/memory/constitution.md` live side by side. Claude reads both. You can later migrate your `CLAUDE.md` rules into the constitution if you want, but there's no rush.

## 5. Pick a script type

During setup you'll see this:

```text
── Choose script type (or press Enter) ──
►  sh (POSIX Shell (bash/zsh))
   ps (PowerShell)
   py (Python)
```

This only changes some helper scripts. It does **not** change how the `/speckit-...` commands work.

| If you use... | Pick |
| --- | --- |
| Git Bash + PowerShell (Windows) | **py** |
| Only PowerShell (Windows) | **ps** |
| Mac or Linux | **sh** |
| Not sure | **py** (works everywhere) |

Use **↑↓ arrow keys** to move, then press **Enter**.

Picked wrong? Just run `specify init --here --force --integration claude` again and pick a different one.

During `specify init`, you'll see this prompt:

```text
── Choose script type (or press Enter) ──
►  sh (POSIX Shell (bash/zsh))
   ps (PowerShell)
   py (Python)
```

This chooses the language of the helper scripts inside `.specify/scripts/`. It does **not** affect the `/speckit-...` slash commands — those always work the same regardless of your choice.

**Recommendation:**

| You are... | Pick | Why |
| --- | --- | --- |
| A Windows user who uses both Git Bash and PowerShell | **py** | Python runs in every terminal on Windows |
| A Windows user who only uses PowerShell | **ps** | Native PowerShell scripts |
| A Mac or Linux user | **sh** | Native shell scripts |
| Not sure | **py** | Safest choice — works everywhere if Python is installed |

Use the **↑↓ arrow keys** to move to your choice, then press **Enter**.

This is a one-time choice per project. If you pick wrong, re-run `specify init --here --force --integration claude` and pick again.

## 6. Check it worked

After setup you should see `Project ready.` in green. Now check these:

**Check 1:** Do the folders exist?

```bash
ls .specify/          # should show: memory/  scripts/  templates/
ls .claude/skills/    # should show: speckit-constitution/  speckit-specify/  etc.
```

**Check 2:** Does the rules file exist?

```bash
ls .specify/memory/   # should show: constitution.md
```

**Check 3:** Does the tool work?

```bash
specify version       # should show a version number
```

If anything is missing, run the setup command again. It only adds what's missing — it won't break what's there:

```bash
specify init --here --force --integration claude
```

"Ensure scripts executable" not ticked? That's a Linux/Mac thing. On Windows it doesn't matter. Everything works.

After `specify init` finishes, you should see `Project ready.` in green. Now check that everything landed correctly.

**Check 1 — folders exist:**

```bash
ls -la .specify/
ls -la .claude/skills/
```

You should see:

- `.specify/` with subfolders: `memory/`, `scripts/`, `templates/`
- `.claude/skills/` with folders like `speckit-constitution/`, `speckit-specify/`, `speckit-plan/`, `speckit-tasks/`, `speckit-implement/`, `speckit-converge/`

**Check 2 — constitution template exists:**

```bash
ls .specify/memory/
```

You should see `constitution.md`. It's a template at this point — you'll fill it with your rules in step 8.

**Check 3 — specify knows this project:**

```bash
specify version
```

This should work from inside the project folder without errors.

**If anything is missing**, the safest fix is to run init again:

```bash
specify init --here --force --integration claude
```

It won't break anything that already exists. It only adds what's missing.

**"Ensure scripts executable" not ticked?** Normal on Windows. That step is for Linux/Mac file permissions. Everything still works.

## 7. Open it in Claude

The `/speckit-...` commands are saved as files in your project. Claude can only see them when it's looking at that folder.

1. Open **Claude Desktop**.
2. Go to the **Code** tab.
3. Open your project folder.
4. Type `/` in the chat — you should see commands like `/speckit-constitution`, `/speckit-specify`, `/speckit-plan`, and more.

If you had old skills (like `debug-issue` from code-review-graph), they still show up too.

**Commands not showing?** Make sure you're in the **Code** tab, not a regular chat.

Spec Kit's slash commands live inside your project folder as files. Claude only sees them when it's working **inside that folder**.

**Step 1:** Open **Claude Desktop** app.

**Step 2:** Switch to the **Code** tab (this runs Claude Code inside the desktop app).

**Step 3:** Open your project folder. Claude should now be pointed at the folder where `.claude/skills/` lives.

**Step 4:** Type `/` in the chat. You should see commands like:

- `/speckit-constitution`
- `/speckit-specify`
- `/speckit-plan`
- `/speckit-tasks`
- `/speckit-implement`
- `/speckit-converge`
- `/speckit-clarify` (optional)
- `/speckit-checklist` (optional)
- `/speckit-analyze` (optional)

If you had existing skills (like `debug-issue`, `review-changes` from code-review-graph), those still appear too. Everything coexists.

**Don't see the commands?** Make sure you're in the **Code** tab, not a regular chat. A regular chat doesn't read `.claude/skills/`.

## 8. Write your rules (constitution)

The constitution is your project's rules. Every Spec Kit command checks them. Write it **once per project**.

In Claude's chat:

```text
/speckit-constitution Code must be clean and easy to read. All APIs need error handling. Write tests. Follow REST style. No passwords in logs.
```

**Already have rules in a `CLAUDE.md` file?** Just tell Claude:

```text
/speckit-constitution Read the CLAUDE.md file and use those rules for the constitution.
```

After Claude writes the file, open `.specify/memory/constitution.md` and read it. If something is off, tell Claude and it will fix it.

**Your project is now fully set up.** You can start building features or fixing bugs.

The constitution is a set of rules that every Spec Kit command will follow. You write it **once per project**.

In Claude's chat (Code tab, project folder open), type:

```text
/speckit-constitution Code must be clean, readable, and well-documented. All APIs must have proper error handling. Write tests for business logic. Follow REST conventions. No sensitive data in logs.
```

Claude creates `.specify/memory/constitution.md` with these rules formatted properly.

**If you already have a `CLAUDE.md` with rules**, point Claude to it:

```text
/speckit-constitution Read the CLAUDE.md file in this project and use those rules as the basis for the constitution.
```

**Read the file after.** Open `.specify/memory/constitution.md` and check it captured what you wanted. If something is wrong, tell Claude in the chat and it will fix it.

**What makes a good constitution:**

- Coding standards: "Use TypeScript strict mode", "Follow PEP 8"
- Testing rules: "Every feature must have unit tests"
- Security rules: "Never log passwords or tokens"
- Architecture rules: "Keep controllers thin, logic in services"
- Team conventions: "Use conventional commits", "Document all public functions"

**After this, your project is fully set up.** You can now use the feature-building flow (`/speckit-specify` → `/speckit-plan` → `/speckit-tasks` → `/speckit-implement` → `/speckit-converge`) or the bug-fixing flow (with the bug extension).

## 9. Add-ons (optional)

Spec Kit has 5 official add-ons. Run these inside your project folder:

| Add-on | What it does | Command |
| --- | --- | --- |
| **bug** | Find, fix, and test a bug in 3 steps | `specify extension add bug` |
| **assess** | Check if an idea is worth building | `specify extension add assess` |
| **git** | Names your branches with numbers like 001-feature | `specify extension add git` |
| **github** | Turns your tasks into GitHub Issues | `specify extension add github` |
| **agent-context** | Gives Claude more info about your project | `specify extension add agent-context` |

See what's installed: `specify extension list`

Remove one: `specify extension remove bug`

There are also 200+ community add-ons (`specify extension search <word>`), but they're not checked by GitHub — have someone experienced review them first.

Spec Kit comes with 5 official extensions that add extra capabilities. Install any of them from Git Bash inside your project folder.

| Extension | What it adds | Install command | Commands you get |
| --- | --- | --- | --- |
| **bug** | Find, fix, and test bugs in 3 steps | `specify extension add bug` | `/speckit-bug-assess`, `/speckit-bug-fix`, `/speckit-bug-test` |
| **assess** | Evaluate an idea before building it | `specify extension add assess` | `/speckit-assess-intake`, `-research`, `-define`, `-shape`, `-decide` |
| **git** | Numbered feature branches (001-feature-name) | `specify extension add git` | Automatic branch naming |
| **github** | Convert tasks.md into GitHub Issues | `specify extension add github` | Tasks become trackable issues |
| **agent-context** | Gives the AI more project context | `specify extension add agent-context` | Richer context in every command |

To see what's installed in your project:

```bash
specify extension list
```

To remove an extension you don't need:

```bash
specify extension remove bug
```

**Community extensions:** There are 200+ community-made extensions. Browse them with `specify extension search <keyword>`. **Warning:** community extensions are not reviewed by GitHub — have a senior developer check the code before installing any of them.

## 10. Git — what to save, what to skip

### Save to GitHub (push these)

| What | Why |
| --- | --- |
| `.specify/memory/constitution.md` | Your rules — the team needs them |
| `.specify/templates/` | Blank forms Spec Kit fills in |
| `.specify/scripts/` | Helper scripts |
| `.specify/extensions.yml` | Which add-ons are installed |
| `.claude/skills/speckit-*/` | The commands for Claude |
| `.claude/settings.json` | Shared settings |
| `specs/` | Your plans and task lists |

### Keep to yourself (don't push)

| What | Why |
| --- | --- |
| `.specify/feature.json` | Tracks *your* current feature — different for each person. Already handled by Spec Kit's `.gitignore`. |
| `.claude/settings.local.json` | Your personal settings |
| `.claude/settings.json.bak` | A backup file |

### Add these two lines to your `.gitignore`

```gitignore
.claude/settings.local.json
.claude/settings.json.bak
```

### First save after setup

```bash
git add .specify/ .claude/ specs/
git commit -m "chore: add Spec Kit setup"
git push
```

### When a teammate gets your repo

They just run `pip install specify-cli` on their computer. The folders are already in the repo, so they don't run `specify init` again.

### Push to GitHub

| File / Folder | Why |
| --- | --- |
| `.specify/memory/constitution.md` | Project rules — everyone follows them |
| `.specify/templates/` | Blank forms Spec Kit uses |
| `.specify/scripts/` | Helper scripts |
| `.specify/extensions.yml` | Which extensions are installed |
| `.specify/.gitignore` | Already created by Spec Kit |
| `.claude/skills/speckit-*/` | Slash commands for Claude |
| `.claude/settings.json` | Shared Claude settings |
| `specs/` | Your feature specs, plans, and tasks |

### Do NOT push

| File | Why | Handled by |
| --- | --- | --- |
| `.specify/feature.json` | Tracks which feature *you* are working on — per developer | Spec Kit's own `.gitignore` |
| `.specify/extensions/*/local-config.yml` | Personal extension settings | Spec Kit's own `.gitignore` |
| `.claude/settings.local.json` | Your personal Claude settings | You add to `.gitignore` |
| `.claude/settings.json.bak` | Backup file | You add to `.gitignore` |

### Add to your project's root `.gitignore`

Spec Kit handles its own files, but add these two lines for Claude's personal files:

```gitignore
# Claude personal files
.claude/settings.local.json
.claude/settings.json.bak
```

### First commit after setup

```bash
git add .specify/ .claude/ specs/
git commit -m "chore: add Spec Kit setup with Claude integration"
git push
```

### When a teammate clones your repo

They don't need to run `specify init` again. The `.claude/skills/` and `.specify/` folders are already in the repo. They just need `pip install specify-cli` to get the `specify` command on their machine, then open the project in Claude Desktop's Code tab.

## 11. Cheat sheet

### New project

```bash
pip install specify-cli                       # once ever
specify init my-app --integration claude        # make the project
cd my-app
/speckit-constitution (your rules)              # in Claude chat
```

### Existing project

```bash
pip install specify-cli                                  # once ever
cd /d/your-project
specify init --here --force --integration claude          # add Spec Kit
/speckit-constitution (your rules)                        # in Claude chat
```

### Add-ons

```bash
specify extension add bug
specify extension add assess
specify extension add git
specify extension add github
```

### Handy commands

```bash
specify version                   # what version is installed
specify self check                # is there a newer version
specify extension list             # what add-ons are installed
pip install --upgrade specify-cli  # get the latest version
```

### New project

```bash
pip install specify-cli                              # once ever
cd /d/projects                                        # go where you want the folder
specify init my-app --integration claude               # creates my-app/ with Spec Kit
cd my-app                                             # enter it
# Open Claude Desktop → Code tab → open my-app/
/speckit-constitution (your rules here)                # in Claude's chat
```

### Existing project

```bash
pip install specify-cli                                        # once ever
cd /d/dms_fullstack/dms_ui                                     # go to your project
git add . && git commit -m "snapshot before Spec Kit"           # save first (optional)
specify init --here --force --integration claude                # add Spec Kit
# Open Claude Desktop → Code tab → open dms_ui/
/speckit-constitution (your rules here)                         # in Claude's chat
```

### Add extensions (optional, run inside the project)

```bash
specify extension add bug        # bug fixing
specify extension add assess     # idea evaluation
specify extension add git        # branch naming
specify extension add github     # GitHub Issues from tasks
```

### Useful commands

```bash
specify version                  # check installed version
specify self check               # check for updates
specify extension list            # see installed extensions
pip install --upgrade specify-cli # upgrade to latest
```
