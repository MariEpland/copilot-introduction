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

### 1. Examine the audit skill template

Open [audit_my_semantic_model.prompt.md](audit_my_semantic_model.prompt.md).

This is a **comprehensive audit skill** that checks:
- Error handling (DIVIDE vs `/`, BLANK handling)
- Naming conventions (descriptive names, consistency)
- Documentation (comments, business context)
- Formatting (formatString for currency and percentages)
- Performance (VAR usage, appropriate aggregation functions)
- Data quality (hard-coded values, type conversions)

**Read through the entire file.** Notice:
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

### 3. Prepare the semantic model for audit

Open [../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl](../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl).

This file contains all the measures you created in exercises 01 and 02:
- Exercise 01 measures (Total Quantity, Orders by Region, Average Order Value, etc.)
- Exercise 02 measures (Total Revenue, YTD Revenue, Product Rank, etc.)

**Review the measures** — remember which ones you completed vs left as BLANK().

### 4. Attach the skill and run the audit

Open Copilot Chat and attach your audit skill:

1. Type `#file` and select `audit_my_semantic_model.prompt.md`
2. Then ask:

```
Audit all DAX measures in ../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl
and generate a comprehensive audit report.

Save the audit report to exercises/powerbi/bonus/audit_report.md
```

**Watch what happens!** Copilot should:
- ✅ Read the measures from the TMDL file
- ✅ Check each measure against the audit checklist
- ✅ Generate a structured audit report
- ✅ Categorize issues as Critical 🔴 / Warning ⚠️ / Good ✅
- ✅ Save the report to `audit_report.md` in this folder

### 5. Review the audit report

Open [audit_report.md](audit_report.md) (Copilot should have created this file).

The report should contain sections like:

- **Executive Summary** — overall health score
- **Critical Issues** — measures that could crash (division by zero, etc.)
- **Warnings** — best practice violations (missing formatString, poor names, etc.)
- **Good Practices** — patterns done well
- **Detailed Findings** — measure-by-measure analysis
- **Recommendations** — prioritized action items

**Read through the findings.** Do they match what you know about the measures?

### 6. (Optional) Update the audit with timestamp

If you want to track audits over time, rename the file:

```powershell
Move-Item audit_report.md "audit_report_$(Get-Date -Format 'yyyy-MM-dd').md"
```

This creates a permanent record with today's date.

### 7. (Optional) Fix the issues

Based on the audit findings, go fix the critical issues!

For example, if the audit flagged measures using `/` instead of DIVIDE:
1. Open [sales_sample.tmdl](../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl)
2. Find the flagged measure
3. Replace `/` with `DIVIDE()` with proper error handling
4. Save the file
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

### Challenge 4: Track improvements over time
1. Run the initial audit (already done in step 4)
2. Fix 3-5 critical issues in the sales_sample.tmdl file
3. Ask Copilot: 
   ```
   Re-audit ../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl
   and save to exercises/powerbi/bonus/audit_report_improved.md
   ```
4. Compare the reports:
   ```
   Compare audit_report.md with audit_report_improved.md and summarize improvements
   ```

---

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
