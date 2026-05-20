# Exercise 05 — Skills & Slash Commands (Power BI)

**Time:** ~10 minutes  
**Goal:** Master Copilot Chat's built-in slash commands and `@workspace` for DAX development.

---

## Background

Copilot Chat has built-in **skills** triggered with slash commands:

| Command | What it does |
|---------|-------------|
| `/explain` | Explains selected DAX in plain English |
| `/fix` | Diagnoses and suggests fixes for DAX errors |
| `/doc` | Generates documentation comments |
| `@workspace` | Searches across your whole project |

---

## Steps

### 1. Open the messy measures file

Open [messy_measures.tmdl](messy_measures.tmdl). It's a collection of undocumented DAX measures with inconsistent style and at least one bug.

Read it — or don't. That's the point of `/explain`.

### 2. Use `/explain`

Highlight one of the complex measures. In Copilot Chat, type:

```
/explain
```

Read the explanation. Does Copilot correctly identify what the measure does? What about the DAX context?

Try highlighting just a portion (like a VAR statement) and run `/explain` again.

### 3. Use `/fix`

The file has at least one buggy measure. Highlight the suspicious one and type:

```
/fix
```

Review the suggested fix. Ask Copilot to explain *why* the original was wrong before applying.

### 4. Use `/doc`

Highlight a measure without a comment. In Copilot Chat, type:

```
/doc
```

Review the generated documentation. Does it accurately describe the business logic?

### 5. Use `@workspace`

In Copilot Chat (with no code highlighted), type:

```
@workspace Where are revenue calculations defined in this project?
```

Copilot should search across all TMDL files and point you to the right measures. Try:

```
@workspace What measures use time intelligence functions?
@workspace Are there any measures that don't handle division by zero?
@workspace How many measures are defined in messy_measures.tmdl?
```

---

## What to Try

- Use `/explain` on a measure using CALCULATE and ask Copilot to explain filter context modifications
- Ask `@workspace`: *"Summarise all the DAX measures defined in this Power BI project."*
- Highlight a confusing measure name and ask: *"Suggest a better name for this measure."*
- Ask Copilot: *"Find all measures that could benefit from VAR for readability."*
- Try `/fix` on multiple buggy measures — does it catch different types of issues?
- Use `/doc` on measures without comments, then ask Copilot to improve the generated documentation
- Combine commands: use `/explain` first, then ask follow-up questions about filter context or performance

---

## Tips

### 📝 Slash Commands Work on Selection

Most slash commands (`/explain`, `/fix`, `/doc`) work best when you **select specific code** first. Select a single measure, a VAR statement, or even just a complex expression to get focused help.

### 🔍 @workspace Searches Everything

`@workspace` becomes powerful in large semantic models with dozens of measures across multiple TMDL files. You can ask questions across all DAX definitions without manually searching.

### 🐛 Multiple Bugs to Find

This file has at least **3 bugs**:
1. `PctGrowth` — uses `/` operator (division by zero risk)
2. `QtyPerOrder` — uses COUNT instead of DISTINCTCOUNT (counts rows, not unique orders)
3. `GrowthPct` — uses `/` operator AND repeats the same CALCULATE twice (inefficient)

Use `/fix` to find and fix them!

---

## Done? 🎉

You've completed all five Power BI exercises! If you have time, head to **exercises/powerbi/bonus/** for a challenge where you'll build your own custom audit skill.
