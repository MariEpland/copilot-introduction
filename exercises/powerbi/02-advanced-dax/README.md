# Exercise 02 — Advanced DAX Challenges (Power BI)

**Time:** ~20 minutes  
**Goal:** Use Copilot Chat to write advanced DAX measures that demonstrate key DAX concepts like iterator functions, CALCULATE, time intelligence, and ranking.

---

## Background

This exercise builds on Exercise 01 by introducing more advanced DAX patterns. You'll work with:
- **Iterator functions** (SUMX, AVERAGEX)
- **Filter modification** (CALCULATE, FILTER)
- **Time intelligence** (TOTALYTD, DATEADD, SAMEPERIODLASTYEAR)
- **Ranking functions** (RANKX, TOPN)
- **Variables** (VAR) for complex calculations

**Key difference from Exercise 01:** This exercise focuses on using **Copilot Chat** to solve business problems, not just completing TODO placeholders.

---

## Steps

### 1. Open the semantic model file

In VS Code, open [sales_sample.tmdl](../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl)

Scroll down to find the "Exercise 02 - Advanced DAX Challenges" section with 8 challenge measures.

### 2. Open the data model reference

Open [data_model.md](data_model.md) in this folder. It describes the tables and columns in the sales_data semantic model.

Keep it open throughout the exercise. Copilot will use it as context when generating DAX.

### 3. Use Copilot Chat to solve each challenge

For each challenge measure:

1. **Read the business requirement** in the comment above the measure
2. **Open Copilot Chat** (`Ctrl+Alt+I`) and describe what you need, for example:

   > "Write a DAX measure for the sales_sample table that calculates total revenue using SUMX, multiplying quantity by VALUE(unit_price)."

3. **Replace `BLANK()`** with the DAX expression Copilot suggests

> **Tip:** Reference `data_model.md` explicitly: *"Using the sales_sample table described in data_model.md, create a measure that..."*

### 4. Ask Copilot to explain DAX concepts

After writing at least three measures, ask Copilot Chat:

> "Explain the difference between SUM and SUMX in DAX. When should I use each one?"

Then ask:

> "What is the difference between row context and filter context in DAX?" 

---

## What to Try

- Ask Copilot: *"Rewrite the Total Revenue measure to handle NULL values in unit_price."*
- Ask Copilot: *"Create a measure that shows the percentage of total revenue for each category."*
- Ask Copilot: *"Explain when to use CALCULATE vs CALCULATETABLE."*
- Try asking Copilot to optimize one of your measures for performance

---

## Testing Your Measures (Optional)

Once you've written a few measures, test them in Power BI Desktop:

1. Save the TMDL file in VS Code
2. Re-open `exercises/powerbi/data/sales_data.pbip` in Power BI Desktop
3. Add the measures to a table or matrix visual
4. Verify the calculations are correct

---

## Done?

Check your answers against [sales_sample_solution.tmdl](sales_sample_solution.tmdl), then move on to **Exercise 03 →**

