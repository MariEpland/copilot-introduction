# Exercise 04 — GitHub Features (Power BI)

**Time:** ~10 minutes  
**Goal:** Use GitHub Copilot features on GitHub.com — PR descriptions and issue assistance — with Power BI DAX code.

---

## Background

Copilot works on GitHub.com too, not just in your editor. It can:
- Generate pull request descriptions from DAX changes
- Help you understand and respond to issues about BI problems

This exercise walks you through fixing a buggy DAX measure, committing it, and letting Copilot write the PR description.

---

## Steps

### 1. Fix the bug

Open [bugfix_measure.tmdl](bugfix_measure.tmdl) in VS Code. The measure has a real bug.

Read the code and try to spot the bug yourself first — then ask Copilot Chat:

> "Does this DAX measure have any bugs? Explain what they are."

Fix the bug (with or without Copilot's help. Hint: Try Agent mode to allow copilot to update your file)

**Hint:** The bug is in the RETURN statement. What happens when `PreviousRevenue` is 0 or BLANK?

### 2. Stage and commit

Open the integrated terminal (`Ctrl+` `` ` ``) and run:

```bash
git add exercises/powerbi/04-github-features/bugfix_measure.tmdl
git commit -m "fix: correct revenue growth calculation to handle null values"
```

### 3. Push to your fork

```bash
git push origin main
```

_(Note: Replace `main` with `master` if your repository uses `master` as the default branch)_

### 4. Open a Pull Request on GitHub

1. Go to your fork on GitHub.com
2. Click **"Compare & pull request"** or go to **Pull requests → New pull request**
3. Set the base repository to **your own fork**, base branch `main` (or `master`)

### 5. Use Copilot to generate the PR description

In the PR creation form, look for the **Copilot icon** (✨) next to the description box.  
Click it → **"Generate with Copilot"**.

Review the generated description. Does it accurately describe the DAX fix? Edit if needed, then submit the PR.

### 6. (Optional) Explore Copilot on an issue

Go to **Issues** tab and create a new issue:

> "The Revenue Growth % measure returns incorrect results when comparing to periods with no sales."

Once created, use Copilot in the issue to ask for solutions.

---

## What to Try

- After the PR is created, go to **Files changed** tab. Hover over the TMDL code — does Copilot offer suggestions?
- Ask Copilot in the issue: *"What are best practices for handling division by zero in DAX?"*
- Try asking Copilot Chat: *"Compare bugfix_measure.tmdl with bugfix_measure_solution.tmdl and explain the fix"*
- Ask Copilot: *"Why should I use DIVIDE() instead of / in DAX?"*

---

## Tip

Copilot's PR quality depends on atomic commits. A commit that fixes one clear issue produces a much better description than a commit changing multiple unrelated things.

---

## Done?

Move on to **Exercise 05 →**
