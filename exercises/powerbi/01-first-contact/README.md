# Exercise 01 — First Contact (Power BI)

**Time:** ~10 minutes  
**Goal:** Get comfortable with Copilot's two core features — inline completions and Copilot Chat — while working with DAX measures in Power BI.

---

## Background

You've been given a Power BI semantic model ([sales_sample.tmdl](../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl)) with several incomplete measure definitions in the sales_sample table. Your job is to finish them **using Copilot**, not by writing the DAX yourself.


If you want you can open `exercises/powerbi/data/sales_data.pbip` in Power BI Desktop to check the state of the file before doing changes. Note that your changes will not be detected by Power BI automtically. After doing changes the file must be re-opened. 
---

## Steps

### 1. Locate the measures file

In VS Code, open [sales_sample.tmdl](../data/sales_data.SemanticModel/definition/tables/sales_sample.tmdl)

Scroll down to find the "Exercise 01" section with TODO measures. Notice the `/// TODO` comments — those are your targets.

### 2. Use inline completions to complete a measure

Go to the `'Total Quantity'` measure. Delete `BLANK()` and **start typing the DAX yourself** — as you type `SUM(`, Copilot will suggest the rest. Press `Tab` to accept.

> **Tip:** If the suggestion isn't right, press `Esc` and try typing a bit more to give Copilot more context. You can also cycle through alternative suggestions with `Alt+]` (Windows/Linux) or `Option+]` (Mac).


### 3. Let a comment guide Copilot

Find the `'Orders by Region'` measure. Notice the TODO comment includes a hint.

Delete `BLANK()` and just press `Enter` to create a new line — Copilot should suggest the entire implementation based on the comment above. Press `Tab` to accept.

> **Tip:** Copilot reads the surrounding context (comments, measure names, hints) to provide smart suggestions even before you start typing.

### 4. Ask Copilot Chat to complete a measure

Highlight the entire `'Average Order Value'` measure definition (including the comments).

Open Copilot Chat (`Ctrl+Alt+I`) and type:

> "Implement this measure to calculate the average revenue per order."

Review the suggestion, then replace `BLANK()` with the suggested DAX.

### 5. Ask Copilot to explain DAX

Highlight the `'Total Sales'` measure (the existing complete measure at the top) and ask Copilot Chat:

> "Explain what this measure does, step by step."

---

## What to Try

Once the TODOs are done, experiment:

- Ask Copilot Chat: *"What's the difference between SUM and SUMX in DAX?"*
- Uncomment the time intelligence measures and ask Copilot to implement them
- Ask Copilot: *"How would I create a measure that shows revenue for the previous month?"*

---

## Testing in Power BI (Optional)

If you want to verify your measures work correctly:

1. Save the TMDL file in VS Code (Best to press File/Save All)
2. Open (or re-open) `exercises/powerbi/data/sales_data.pbip` in Power BI Desktop
3. Create a visual and add your measures to test them

> **Note:** Power BI Desktop does not automatically detect TMDL file changes while open. You must save .tmdl and .pbip file and re-open the PBIP file to see your updates.

---

## Done?

Check your work against [sales_sample_solution.tmdl](sales_sample_solution.tmdl) (which shows the complete table with all measures implemented), then move on to **Exercise 02 →**
