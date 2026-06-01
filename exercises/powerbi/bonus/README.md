# Bonus Exercise — Create Your Own Audit Skill

**Time:** ~20 minutes (for fast finishers)  
**Goal:** Build a custom **"audit_my_semantic_model"** skill that performs comprehensive DAX quality audits, then use it to audit the sales_sample semantic model.

---

## Background

In Exercise 05, you mastered Copilot's built-in slash commands (`/explain`, `/fix`, `/doc`, `@workspace`). Now you'll take the next step: **creating your own custom skill**.

This exercise teaches you to build an **audit skill** that systematically reviews an entire semantic model for:

- 🐛 Critical issues (crashes, errors)
- ⚠️ Best practice violations
- ✅ Good patterns worth recognizing
- 📊 Performance optimization opportunities

This is the kind of skill you could use on real projects with dozens or hundreds of measures to maintain quality standards across a team.

---

## Steps

### 1. Examine the audit skill

Open [audit-data-model/skill.md](audit-data-model/skill.md).

This is a **comprehensive audit skill** that checks:
- Error handling (DIVIDE vs `/`, BLANK handling)
- Naming conventions (descriptive names, consistency)
- Documentation (comments, business context)
- Formatting (formatString for currency and percentages)
- Performance (VAR usage, appropriate aggregation functions)
- Data quality (hard-coded values, type conversions)

**Read through the entire file.** Notice:
- The YAML frontmatter (`name` and `description`)
- The detailed checklist (6 categories)
- The structured audit report format
- The response style guidelines

### 2. Customize the skill (optional)

You can add your own audit rules! For example, add to the checklist:

```markdown
### 7. **Display Folder Organization**
- ✅ Check: Are related measures grouped in display folders?
- ⚠️ Flag: Time intelligence measures not in "Time Intelligence" folder
- ⚠️ Flag: More than 10 measures at root level without organization
```

Or add a rule about specific DAX patterns your team uses.

**Save your changes** if you customize it.

### 3. Inspect the Power BI model 

You can inspect the semantic model in two ways:

**Option A — Open in Power BI Desktop:**

Open the PBIP project: [Sales_sample.pbip](Sales_sample.pbip)

> ⚠️ **Before opening**, you must update the Power Query source path to point to `sales_sample.csv` on your computer.
>
> Open [sales_sample.tmdl](Sales_sample.SemanticModel/definition/tables/sales_sample.tmdl) and find the `File.Contents(...)` line in the partition query. Replace the path with the actual location where you saved the file, e.g.:
> ```
> File.Contents("C:\your\path\to\sales_sample.csv")
> ```

**Option B — Inspect the TMDL file directly:**

Open [sales_sample.tmdl](Sales_sample.SemanticModel/definition/tables/sales_sample.tmdl) in VS Code. All measures and their definitions are visible as plain text.

The semantic model contains measures that intentionally violate best practices:
- Measures with poor names (`rev`, `X`, `avg`)
- Division without DIVIDE() (division by zero risk)
- Missing formatStrings and documentation
- Repeated calculations without VAR
- Hard-coded filter values

### 4. Create your audit skill

In this step you'll create a reusable prompt (skill) and place it under `.github/skills/` in the workspace. Choose one approach:

**Option A — Copy the provided skill:**
1. Create the folder `.github/skills/audit-data-model/` in the workspace root
2. Copy `audit-data-model/skill.md` from this exercise folder into it

**Option B — Write your own from scratch:**
1. Create `.github/skills/audit-data-model/skill.md`
2. Add YAML frontmatter with `name` and `description`
3. Write your own audit checklist and report format (use the provided skill as inspiration)

**Option C — Ask Copilot to generate one:**
1. Open Copilot Chat and ask:
   > "Create a skill file at `.github/skills/audit-data-model/skill.md` that audits DAX measures for error handling, naming, documentation, formatting, and performance issues. Use YAML frontmatter with name and description."
2. Review and tweak the output

---

### 5. Run the audit

**Start a new Copilot Chat session** (Ctrl+L) so it picks up the new skill.

1. Type `/audit-data-model`
2. Attach the semantic model file: type `#file` and select `exercises/powerbi/bonus/Sales_sample.SemanticModel/definition/tables/sales_sample.tmdl`
3. Then ask:

```
Audit all DAX measures in the attached sales_sample.tmdl file
and generate a comprehensive audit report.

Save the audit report to exercises/powerbi/bonus/audit_report.md
```

**Watch what happens!** Copilot should:
- ✅ Read the measures from the TMDL file
- ✅ Check each measure against the audit checklist
- ✅ Generate a structured audit report
- ✅ Categorize issues as Critical 🔴 / Warning ⚠️ / Good ✅
- ✅ Save the report to `audit_report.md` in this folder

### 6. Review the audit report

Open [audit_report.md](audit_report.md) (Copilot should have created this file).

The report should contain sections like:

- **Executive Summary** — overall health score
- **Critical Issues** — measures that could crash (division by zero, etc.)
- **Warnings** — best practice violations (missing formatString, poor names, etc.)
- **Good Practices** — patterns done well
- **Detailed Findings** — measure-by-measure analysis
- **Recommendations** — prioritized action items

**Read through the findings.** Do they match what you know about the measures?



### 7. (Optional) Fix the issues

Based on the audit findings, go fix the critical issues! Use Copilot to do this. 

For example, if the audit flagged measures using `/` instead of DIVIDE:
1. Open [sales_sample.tmdl](Sales_sample.SemanticModel/definition/tables/sales_sample.tmdl)
2. Find the flagged measure (e.g., `X`, `avg`, `GrowthPct`)
3. Replace `/` with `DIVIDE()` with proper error handling
4. Save the file and re-open the `.pbip` in Power BI Desktop
5. **Re-run the audit** to verify the fix

You can iterate: audit → fix → audit → fix until you achieve a 🟢 Good rating!

---

## What to Observe

- **Thoroughness:** Does the audit catch all the issues you remember from the exercises?
- **Prioritization:** Does it correctly identify critical issues vs style issues?
- **Actionability:** Are the recommendations specific and fixable?
- **Coverage:** Does it audit all measure categories (base, time intelligence, etc.)?

---

## Stretch Goals

If you finish early, try these advanced challenges:

### Challenge 1: Audit another model
Audit the messy measures from Exercise 05:

```
Audit all DAX measures in ../05-skills/messy_measures.tmdl
and save the report to exercises/powerbi/bonus/audit_report_messy_measures.md
```

Does the audit catch the 3 bugs from Exercise 05?

### Challenge 2: Extend the skill with automation
Add a rule to your skill that suggests specific fixes:

```markdown
## Auto-Fix Suggestions

For common issues, provide exact DAX code to replace:

**Issue:** Uses `/` operator
**Fix:** Replace `(a - b) / b` with `DIVIDE(a - b, b, BLANK())`
```

### Challenge 3: Create a compliance matrix
Ask Copilot (with the skill attached):

```
Create a compliance matrix showing which measures pass/fail each audit category
```


---

## Tips

### 🎯 Skills Make Copilot an Expert

By attaching `audit_my_semantic_model.prompt.md`, you're teaching Copilot to think like a **BI auditor**. Without the skill, Copilot gives general advice. With the skill, it applies your specific audit framework systematically.

### 📋 Audits Work Best on Complete Models

The skill performs best when auditing completed measures (not BLANK() placeholders). If you didn't finish exercises 01-02, complete a few more measures first, then run the audit.

### 🔄 Iterate Until Clean

Professional semantic models go through multiple audit cycles:
1. **Initial audit** → Find all issues
2. **Fix critical issues** → Address crashes and errors
3. **Re-audit** → Verify fixes, find remaining warnings
4. **Fix warnings** → Address best practices
5. **Final audit** → Achieve 🟢 Good rating

This is exactly how real BI teams maintain quality!

### 💾 Save Audit Reports

Audit reports are valuable documentation:
- Track quality improvements over time
- Onboard new team members (show them common issues)
- Justify refactoring work to stakeholders
- Catch regressions (compare new audit vs old audit)

### 🛠️ Customize for Your Team

The skill template is a starting point. Add your team's specific rules:
- "All customer-related measures must be in 'Customer Analytics' folder"
- "Revenue measures must reference [Total Revenue] base measure, not recalculate"
- "KPI measures must include target comparison and variance"

---

## Real-World Application

This audit skill pattern works on production semantic models with hundreds of measures:

```
Audit all DAX measures in MyCompanyModel.SemanticModel/definition/tables/*.tmdl
Focus on critical issues only (crashes, performance problems)
Generate summary statistics by audit category
```

Teams use this for:
- 📊 **Quality gates** — Block PRs with critical audit failures
- 🎓 **Learning** — New BI developers learn patterns from audit feedback
- 🔍 **Technical debt** — Quantify and prioritize cleanup work
- ✅ **Compliance** — Ensure models meet company standards

---

## Done? 🎉

Congratulations! You've completed all Power BI exercises and built a production-ready audit skill!

**What you learned:**
- ✅ Copilot inline completions and chat (Exercise 01)
- ✅ Advanced DAX with Copilot assistance (Exercise 02)
- ✅ Custom instructions for team standards (Exercise 03)
- ✅ GitHub integration for PRs and issues (Exercise 04)
- ✅ Slash commands and creating basic skills (Exercise 05)
- ✅ Building comprehensive audit skills (Bonus)

**Next steps:**
- Apply these techniques to your real Power BI projects
- Share the audit skill with your team
- Create more specialized skills (e.g., time intelligence patterns, performance optimization)
- Set up `.github/copilot-instructions.md` in your production repositories
