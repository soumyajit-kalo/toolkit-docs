# EGM Install Guide for MacBook Pro (macOS)

**EGM = Elephant-Goldfish Model**, an open-source plugin from Google
(source: https://github.com/google/elephant-goldfish-model)

---

## What is EGM?

EGM is an **add-on (plugin) for Claude Code**. It helps you **plan** your code before you write it.

- 🐘 **Elephant**: Claude, with your project's history, writes a plan for a feature.
- 🐟 **Goldfish**: fresh Claude helpers that haven't seen your chat check the plan for mistakes.
- 🧑 **You**: decide what to build.

EGM is **not** a separate program. It goes **inside** Claude Code.
So the job is: **make sure Claude Code is ready, then add the plugin.**

---

## Prerequisites (things you need)

| Need | Why | How to check |
|---|---|---|
| MacBook Pro with macOS | Your computer | Already have it ✅ |
| Internet connection | To download EGM from GitHub | Open any website |
| Git | Downloads code from GitHub | `git --version` |
| Claude Code (version **2.1.271 or later**) | EGM runs inside it | `claude --version` |
| Claude Desktop app | Where you code | Download from claude.ai if needed |

---

## Step 1: Open Terminal

1. Press **Cmd + Space** to open Spotlight search.
2. Type `Terminal`.
3. Press **Enter**.

A window opens. You will type the commands below in it and press **Enter** after each one.

---

## Step 2: Check that Git is installed

Git is a tool that downloads code from GitHub. EGM comes from GitHub.

```bash
git --version
```

- ✅ If you see something like `git version 2.39.5`, Git is installed. Go to **Step 3**.
- ❌ If your Mac shows a pop-up asking to install **"command line developer tools"**, click **Install** and wait until it finishes.

You can also start that install yourself with:

```bash
xcode-select --install
```

Then check again:

```bash
git --version
```

---

## Step 3: Check that Claude Code is installed

```bash
claude --version
```

- ✅ If you see a version number, go to **Step 4**.
- ❌ If you see `command not found`, install Claude Code:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Close and reopen Terminal**, then check again:

```bash
claude --version
```

---

## Step 4: Make sure Claude Code is new enough

EGM needs **version 2.1.271 or later**.
If your version number is lower, update it:

```bash
claude update
```

Then check again with `claude --version`.

---

## Step 5: Add the EGM "shop" (marketplace)

```bash
claude plugin marketplace add google/elephant-goldfish-model
```

This tells Claude Code where to find EGM on GitHub.

---

## Step 6: Install EGM

```bash
claude plugin install egm@egm
```

---

## Step 7: Turn EGM on

```bash
claude plugin enable egm@egm
```

If it says EGM is already enabled, that's fine. ✅

---

## Step 8: Restart and test

1. **Fully quit** the Claude app (press **Cmd + Q**).
2. Open it again.
3. Start a **new** coding session in your project.
4. Type:

```text
/egm:egm-brainstorm Add a login page to this project.
```

### If `/egm:` commands don't show up in the Desktop app

Use Terminal instead:

```bash
cd ~/path/to/your/project
claude
```

Then type the same `/egm:` command there.

---

## Mac tip: allow permissions

Claude may ask permission to read EGM's files. Click **Allow**.
These are EGM's own instruction files, stored here:

```text
~/.claude/plugins/cache/egm/
```

---

## Your first easy test

The simplest way to try EGM is to review a file you already have, like your README:

```text
/egm:egm-review README.md
```

---

## What each EGM command does

| Command | What it does |
|---|---|
| `/egm:egm-brainstorm` | Talk through an idea and save a short plan |
| `/egm:egm-draft` | Turn that plan into a design document |
| `/egm:egm-review` | Have fresh Goldfish helpers check the document |
| `/egm:egm-lite` | A faster version for small fixes |
| `/egm:egm-drift-report` | Check if your documents still match your code |

---

## Good to know

- **code-review-graph**: EGM works separately from it, so they don't conflict. You can keep using both.
- **Usage limits**: EGM sends many helper agents at once, so it can use up your Claude usage limits faster than normal chatting.
- **Errors?** Copy the exact error message and ask for help.

---

## Quick command summary (copy-paste)

```bash
git --version
claude --version
claude update
claude plugin marketplace add google/elephant-goldfish-model
claude plugin install egm@egm
claude plugin enable egm@egm
```
