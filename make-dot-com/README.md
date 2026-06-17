# ⚙️ Make.com Automations
### AI-Powered Workflow Automations | Built with Make.com + Groq API

[![Make.com](https://img.shields.io/badge/Make.com-6D00CC?style=flat&logo=make&logoColor=white)](https://make.com)
[![Groq](https://img.shields.io/badge/Groq-FF6B35?style=flat&logoColor=white)](https://groq.com)
[![LLM](https://img.shields.io/badge/LLM-llama--3.3--70b-blue?style=flat)](https://groq.com)
[![Google Workspace](https://img.shields.io/badge/Google_Workspace-4285F4?style=flat&logo=google&logoColor=white)](https://workspace.google.com)
[![Slack](https://img.shields.io/badge/Slack-4A154B?style=flat&logo=slack&logoColor=white)](https://slack.com)

---

## 🧠 Platform Overview

All automations in this folder are built on **Make.com** (formerly Integromat) as the orchestration layer, with **Groq's free API** (`llama-3.3-70b-versatile`) as the AI brain.

The focus is on solving real pain points for **agile delivery teams** — standup reporting, sprint ceremonies, meeting follow-ups, client visibility, and escalation management.

---

## 🛠️ Core Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| **Automation Platform** | Make.com | Workflow orchestration & module chaining |
| **AI / LLM** | Groq API (llama-3.3-70b-versatile) | Text summarisation, classification, structuring |
| **Input** | Google Forms | Structured data collection from team members |
| **Storage** | Google Sheets | Data persistence, deduplication, logging |
| **Output — Email** | Gmail | Formatted summary delivery |
| **Output — Chat** | Slack | Real-time alerts and escalation notifications |

---

## ✅ Automations Built

| # | Name | Modules | Problem Solved |
|---|---|---|---|
| [01](./automation-01-standup-summariser/) | Daily Standup Summariser | 6 | Manual standup note-taking & distribution |
| [02](./automation-02-weekly-status-report/) | Weekly Status Report Generator | 6 | Hours spent compiling weekly team reports |
| [03](./automation-03-meeting-action-tracker/) | Meeting Action Item Tracker | 6 | Action items lost or forgotten after meetings |
| [04](./automation-04-sprint-retro-summariser/) | Sprint Retro Summariser | 8 | Unstructured retro outputs, missing follow-ups |
| [05](./automation-05-blocker-escalation-bot/) | Blocker Escalation Bot | 21+ | Blockers not escalated on time, no visibility |

---

## 🔁 Common Automation Pattern

All Make.com automations in this portfolio follow a consistent architectural pattern:

```
Trigger (Form / Schedule / Manual)
    ↓
Google Sheets — Read & Filter
    ↓
Text Aggregator — Combine entries
    ↓
HTTP Module — Groq API (AI processing)
    ↓
Router (if needed) — Conditional logic
    ↓
Output — Gmail / Slack / Google Sheets
```

---

## 🧩 Key Technical Patterns & Learnings

### Variable Visibility Workaround
Variables set in modules before a Text Aggregator become invisible in downstream variable pickers. **Fix:** Add a `Google Sheets → Get a Row` module after the AI response step to re-expose mapped variables.

### Groq API Response Mapping
Correct path to extract AI response content:
```
data → choices → [] → message → content
```

### Monday Date Calculation (Make.com)
```
addDays(startOfWeek(now); 1)
```

### Gmail HTML Formatting
To preserve line breaks in Gmail output:
```html
<pre style="white-space: pre-wrap;">{{ai_response}}</pre>
```

### Deduplication Pattern
Use a `Processed` column in Google Sheets + filter condition to avoid reprocessing submitted entries.

---

## 📈 Complexity Progression

```
#01 Standup Summariser     ████░░░░░░  Basic
#02 Weekly Report          ████░░░░░░  Basic
#03 Action Item Tracker    █████░░░░░  Intermediate
#04 Retro Summariser       ██████░░░░  Intermediate
#05 Blocker Escalation     ██████████  Advanced (21+ modules, Slack + Gmail)
```

---

## 💡 Consulting Insight

> These automations were not built as demos — they mirror real workflows from active project delivery experience. Each one addresses a specific bottleneck that agile teams face daily, and can be configured and deployed for any team within days.

---

*Part of the [AI Automation Consulting Portfolio](../README.md) by Allavudeen S*
