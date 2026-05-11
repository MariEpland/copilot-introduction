# Exercise 02 — DAX Assistant

**Time:** ~10 minutes  
**Goal:** Use Copilot Chat to write DAX measures for a Power BI data model based on the sales dataset.

---

## Background

DAX (Data Analysis Expressions) is the formula language used in Power BI, Excel, and Fabric. Writing DAX from scratch requires knowing a lot of function names and evaluation context rules — exactly the kind of thing Copilot is great at.

Your job is to write the measures in `challenges.dax` using **Copilot Chat**, not from memory.

The data model is described in `data_model.md` — open it first.

---

## Steps

### 1. Open the data model description

Open `data_model.md`. It describes the three tables and their relationships — the same sales domain as the rest of this repo.

Keep it open throughout the exercise. Copilot will use it as context.

### 2. Open the challenges file

Open `challenges.dax`. Each challenge is a block comment describing a business requirement, followed by an empty measure definition.

### 3. Use Copilot Chat to write each measure

For each challenge:
1. Read the business requirement comment.
2. Open Copilot Chat and describe what you need, for example:

   > "Write a DAX measure that calculates total revenue as quantity times unit price, using the Orders and Products tables."

3. Paste the result into the file and adjust if needed.

> **Tip:** Paste the relevant part of `data_model.md` into the chat for better results. Or just say *"using the data model in data_model.md"* — with that file open, Copilot can reference it.

### 4. Ask Copilot to explain evaluation context

DAX's biggest gotcha is **row context vs. filter context**. After writing at least two measures, ask Copilot Chat:

> "Explain the difference between row context and filter context in DAX, using my measures as an example."

---

## What to Try

- Ask Copilot: *"Rewrite my Total Revenue measure using SUMX instead of a pre-calculated column."*
- Ask Copilot: *"What is the difference between CALCULATE and CALCULATETABLE?"*
- Ask Copilot: *"Add a measure that shows revenue for the previous year using SAMEPERIODLASTYEAR."*

---

## Tip

DAX measures live inside a Power BI model — you can't run this file directly. Think of `challenges.dax` as your **drafting pad**: write and refine the DAX here with Copilot's help, then paste it into Power BI Desktop or Fabric when you're ready.

---

## Done?

Check your answers against `challenges_solution.dax`, then move on to **Exercise 03 →**
