# 📊 Automation #02 — Weekly Status Report Generator
### Automatically compile and deliver AI-formatted weekly team status reports

[![Make.com](https://img.shields.io/badge/Make.com-6D00CC?style=flat&logo=make&logoColor=white)](https://make.com)
[![Groq](https://img.shields.io/badge/Groq-FF6B35?style=flat&logoColor=white)](https://groq.com)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)](https://sheets.google.com)
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white)](https://gmail.com)

---

## 🚨 Problem Statement

Every Friday, project managers spend 30–60 minutes manually pulling standup data from the week, compiling it per team member, formatting it into a report, and sending it to stakeholders. This is pure manual overhead — repetitive, time-consuming, and error-prone.

**This automation does it in seconds.**

---

## ✅ Solution

On a scheduled trigger (or manual run), the automation pulls the entire week's standup entries from Google Sheets, aggregates them by team member, sends them to **Groq AI** for structured summarisation, and delivers a polished **HTML-formatted email** to the team and stakeholders.

---

## 🔁 Workflow

```
Manual / Scheduled Trigger (Friday)
        ↓
Google Sheets (Fetch week's standup entries)
        ↓
Text Aggregator (Combine: Member / Yesterday / Today / Blockers / Date)
        ↓
Set Variable — cleanText
        ↓
HTTP Module → Groq API (AI weekly summary, member attribution)
        ↓
Gmail (Send HTML-formatted weekly status report)
```

---

## 🧩 Module Breakdown

| # | Module | Purpose |
|---|---|---|
| 1 | Manual Trigger | Run on demand every Friday |
| 2 | Google Sheets — Search Rows | Fetch current week's entries |
| 3 | Text Aggregator | Combine all entries with member + date context |
| 4 | Set Variable (cleanText) | Sanitise for AI input |
| 5 | HTTP — Groq API | Generate structured weekly summary |
| 6 | Gmail — Send Email | Deliver HTML report to stakeholders |

---

## 🤖 AI Prompt Used

```
You are a project reporting assistant for an agile delivery team.

Below are daily standup entries from the week. Summarise the week's work 
per team member in a clear, professional weekly status report.

For each team member include:
- Key accomplishments this week
- Work in progress
- Blockers encountered (if any)

Format the output as a clean, readable report suitable for stakeholder communication.
Keep it concise and attribute all points to the correct team member.

Weekly Standup Data:
{{cleanText}}
```

---

## 🗂️ Google Sheet Structure

| Column | Purpose |
|---|---|
| Timestamp | Entry date and time |
| Name | Team member name |
| Yesterday | Previous day's work |
| Today | Planned work |
| Blockers | Any blockers |
| Processed | Deduplication flag |

---

## ⚙️ Technical Notes

- **Trigger:** Manual (run every Friday) — can be switched to scheduled
- **Date filter:** Uses `addDays(startOfWeek(now); 1)` to correctly anchor to Monday
- **Groq Model:** `llama-3.3-70b-versatile`
- **Temperature:** 0.4 (slightly creative for narrative-style reporting)
- **API Response Path:** `data → choices → [] → message → content`
- **Gmail formatting:** `<pre style="white-space: pre-wrap;">` to preserve line breaks in HTML email

---

## 📧 Sample Output Structure

```
Weekly Status Report — Week of [Date]

👤 John (Developer)
  ✅ Completed API integration for payment module
  🔨 Working on unit test coverage
  🚨 Blocked on QA environment access

👤 Priya (QA Lead)
  ✅ Completed regression test suite for v2.1
  🔨 Reviewing test cases for new features
  🚨 None
```

---

## 💡 Consulting Insight

> Weekly reporting is one of the highest-ROI automations for any delivery team. It removes a recurring Friday bottleneck for PMs and gives stakeholders consistent, on-time visibility. Estimated time saving: **2–3 hours/week** for a team of 5–8 members.

---

## 📸 Screenshots

*(Coming soon — Make.com scenario blueprint screenshot)*

---

*Part of the [Make.com Automation Suite](../README.md) | [Back to Portfolio](../../README.md)*
