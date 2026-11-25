# EGM Install Guide for Windows 11

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
| Windows 11 | Your computer | Already have it ✅ |
| Internet connection | To download EGM from GitHub | Open any website |
| Git | Downloads code from GitHub | `git --version` |
| Claude Code (version **2.1.271 or later**) | EGM runs inside it | `claude --version` |
| Claude Desktop app | Where you code | Already have it ✅ |

---

## Step 1: Open PowerShell

1. Press the **Windows key** on your keyboard.
2. Type `PowerShell`.
3. Click **Windows PowerShell**.

A blue or black window opens. You will type the commands below in it and press **Enter** after each one.

---

## Step 2: Check that Git is installed

Git is a tool that downloads code from GitHub. Claude Code needs it, and EGM comes from GitHub.

```powershell
git --version
```

- ✅ If you see something like `git version 2.47.0`, Git is installed. Go to **Step 3**.
- ❌ If you see an error, install Git:

```powershell
winget install --id Git.Git -e
```

Then **close PowerShell, open it again**, and run this to confirm:

```powershell
git --version
```

---

## Step 3: Check that Claude Code is installed

The Claude Desktop app has Claude Code inside it, but you also need the `claude` command in PowerShell to install plugins.

```powershell
claude --version
```

- ✅ If you see a version number, go to **Step 4**.
- ❌ If you see an error, install Claude Code:

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Close and reopen PowerShell**, then check again:

```powershell
claude --version
```

---

## Step 4: Make sure Claude Code is new enough

EGM needs **version 2.1.271 or later**.
If your version number is lower, update it:

```powershell
claude update
```

Then check again with `claude --version`.

---

## Step 5: Add the EGM "shop" (marketplace)

```powershell
claude plugin marketplace add google/elephant-goldfish-model
```

This tells Claude Code where to find EGM on GitHub.

---

## Step 6: Install EGM

```powershell
claude plugin install egm@egm
```

---

## Step 7: Turn EGM on

```powershell
claude plugin enable egm@egm
```

If it says EGM is already enabled, that's fine. ✅

---

## Step 8: Restart and test

1. **Fully close** the Claude Desktop app.
2. Open it again.
3. Start a **new** coding session in your project.
4. Type:

```text
/egm:egm-brainstorm Add a login page to this project.
```

### If `/egm:` commands don't show up in the Desktop app

Use PowerShell instead:

```powershell
cd C:\path\to\your\project
claude
```

Then type the same `/egm:` command there.

---

## Windows tip: allow permissions

Claude may ask permission to read EGM's files. Click **Allow**.
These are EGM's own instruction files, stored here:

```text
C:\Users\<your name>\.claude\plugins\cache\egm\
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

```powershell
git --version
claude --version
claude update
claude plugin marketplace add google/elephant-goldfish-model
claude plugin install egm@egm
claude plugin enable egm@egm
```
