# Introduction to GitHub Copilot

Welcome to the hands-on portion of the **Introduction to GitHub Copilot** session.

This repository contains five guided exercises (plus a bonus) that take you from your first Copilot autocomplete all the way to exploring GitHub.com features and custom instructions.

---

## Prerequisites

Before you start, make sure you have:

- [ ] **VS Code** installed ([code.visualstudio.com](https://code.visualstudio.com))
- [ ] **GitHub Copilot extension** installed in VS Code (`GitHub.copilot` + `GitHub.copilot-chat`)
- [ ] A **GitHub account with Copilot access** (your company license)
- [ ] **Git basics** done (clone, commit, push, pull requests)
- [ ] **Python 3.8+** installed (check with `python --version`)

---

## Getting Started

1. **Fork** this repository to your own GitHub account (button top-right on GitHub)
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/copilot-introduction.git
   cd copilot-introduction
   ```
3. **Open in VS Code**:
   ```bash
   code .
   ```
4. Open the Copilot Chat panel (the chat bubble icon in the left sidebar, or `Ctrl+Alt+I`)
5. You're ready — start with **Exercise 01** below!

---

## Exercises

Work through these in order. Each exercise has its own `README.md` with step-by-step instructions.

| # | Folder | Title | What you'll practise |
|---|--------|-------|----------------------|
| 01 | `exercises/01-first-contact/` | First Contact | Inline completions + Copilot Chat basics |
| 02 | `exercises/02-dax-assistant/` | DAX Assistant | Write DAX measures for a Power BI data model |
| 03 | `exercises/03-custom-instructions/` | Custom Instructions | Teach Copilot about your project |
| 04 | `exercises/04-github-features/` | GitHub.com Features | Copilot on pull requests & issues |
| 05 | `exercises/05-skills/` | Skills & Slash Commands | `/explain`, `/fix`, `/tests`, `@workspace` |
| 🎁 | `exercises/bonus/` | Agent Mode Pipeline | Open-ended: build an ETL script with Agent Mode |

Each exercise takes roughly **10 minutes**. The bonus is open-ended — jump in if you finish early.

---

## Tips

- **Tab** accepts an inline suggestion. **Esc** dismisses it.
- Open Copilot Chat with `Ctrl+Alt+I` (Windows/Linux) or `Cmd+Option+I` (Mac).
- Highlight code, right-click → **Copilot** to access quick actions.
- If a suggestion isn't great, try rephrasing your comment or prompt — context matters.
- Copilot learns from the files open in your editor. Keep relevant files open!

---

## Data

All exercises share a common dataset in `data/sales_sample.csv` — a small fictional sales table with orders, customers, products, and regions. You don't need to load it anywhere; the exercises will point you to it as needed.
