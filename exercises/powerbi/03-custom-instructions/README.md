# Exercise 03 — Custom Instructions (Power BI)

**Time:** ~10 minutes  
**Goal:** Set up Power BI-specific custom instructions in `.github/copilot-instructions.md` and observe how they improve DAX suggestions.

---

## Background

Custom instructions let you teach Copilot about *your* Power BI development practices — DAX patterns, naming conventions, measure organization, and what to avoid. Copilot Chat automatically includes this file in every conversation within the workspace.

This is like briefing a new BI developer on your team's standards.

---

## Steps

### 1. Test WITHOUT custom instructions

First, let's see how Copilot behaves without any custom instructions.

Open Copilot Chat and ask:

> "Write a measure that calculates the percentage of total sales contributed by the current product"

**Observe:**
- What did it name the measure?
- Does it include a `///` description comment?
- Does it include a `formatString`?
- Does it add a `displayFolder` annotation?
- Is the output in TMDL format or just raw DAX?

Keep this response visible for comparison.

---

### 2. Copy and customize the template

Now create your custom instructions file.

A Power BI-specific template is provided in this exercise folder.

Copy `instructions_template_powerbi.md` to `.github/copilot-instructions.md` in the workspace root. If the `.github` folder doesn’t exist in your repo, you can create it manually.

Then open `.github/copilot-instructions.md` and make at least **three changes** that reflect your Power BI development preferences:

- ✏️ Add a rule: **"Always output DAX measures in TMDL format (with measure keyword, formatString, and lineageTag placeholder)"**
- ✏️ Add a rule: **"Always include a `///` description comment above each measure explaining the business purpose"**
- ✏️ Add a naming convention: **"Prefix percentage measure names with `% ` (e.g., `% Product Contribution`)"**
- ✏️ Add a formatting rule: **"Percentage measures must use `formatString: 0.0%`"**
- ✏️ Add a display folder rule: **"Assign percentage/KPI measures to `displayFolder: KPIs`"**

**Save the file** when done.

---

### 3. Test AGAIN with custom instructions

Now test the same prompt with your custom instructions in place.

**Important:** Start a **new Copilot Chat conversation** (click the + button or use Ctrl+L) so Copilot loads your new instructions file.

Ask the **exact same question**:

> "Write a measure that calculates the percentage of total sales contributed by the current product"

**Compare:**
- Does it now use your naming convention (e.g., `% Product Contribution`)?
- Does it include a `///` description comment above the measure?
- Does it include `formatString: 0.0%`?
- Does it add `displayFolder: KPIs`?
- Is it now in TMDL format?

---

### 4. Ask Copilot to reflect on its instructions

In Copilot Chat, ask:

> "What DAX conventions should I follow in this project?"

Copilot should reflect back your custom instructions from the `.github/copilot-instructions.md` file.

---

## What to Try

Experiment with different types of custom instructions and observe the before/after difference:

- **Test domain vocabulary:** Add this rule: *"Revenue means quantity × unit_price. Order value means the sum of revenue for a single order_id."* — then test before/after with: *"Calculate average order value"*
- **Test display folders:** Add this rule: *"Put time intelligence measures in a 'Time Intelligence' display folder"* — then ask Copilot to create a YTD Revenue measure and check if it adds the folder annotation
- **Test formatting standards:** Add this rule: *"Currency measures must use '$#,##0.00' format, percentages must use '0.0%'"* — then ask for a revenue measure and a percentage measure
- **Get feedback:** Ask Copilot: *"Review my custom instructions for Power BI and suggest improvements"*

**Remember:** Always start a **new Copilot Chat conversation** after editing `.github/copilot-instructions.md` so the changes are loaded!

---

## Example Custom Rules

Here are some Power BI-specific rules you might want to add:

```markdown
## DAX Conventions

- Always use DIVIDE() instead of / to handle division by zero
- Use SUMX/AVERAGEX/COUNTX for row-level calculations, SUM/AVERAGE/COUNT for simple aggregations
- Prefer ISBLANK() over = BLANK() for null checks
- Use VAR for intermediate calculations to improve readability
- Always format currency measures with "$#,##0.00"
- Always format percentage measures with "0.0%"

## Measure Naming

- Prefix aggregations: "Total Sales", "Count Orders"
- Prefix time intelligence: "YTD Sales", "MTD Orders"
- Prefix percentages: "% of Total", "% Growth"
- Use descriptive names: avoid abbreviations unless industry-standard

## Measure Organization

- Group related measures in display folders
- Put base measures (Total Revenue, Total Quantity) at the root
- Put time intelligence in "Time Intelligence" folder
- Put KPIs in "KPIs" folder
```

---

## Tips

### 📝 Be Specific and Actionable

Custom instructions are most effective when **specific and actionable**. Vague rules like "write good DAX" have little impact. Concrete patterns like "use SELECTEDVALUE for single-value contexts" produce consistent results.

### 🔄 Test Before and After

The best way to validate your custom instructions is to:
1. Ask a question **before** creating the file
2. Add your custom rules
3. Start a **new chat** and ask the **same question**
4. Compare the responses side-by-side

### 🆕 Reload Instructions

**Important:** Copilot loads `.github/copilot-instructions.md` when starting a new chat conversation. After editing the file, click the **+ button** in Copilot Chat or press **Ctrl+L** to start fresh and pick up your changes.

---

## Done?

Move on to **Exercise 04 →**
