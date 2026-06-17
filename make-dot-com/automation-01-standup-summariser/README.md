# 📋 Automation #01 — Daily Standup Summariser
### Automatically collect, summarise, and distribute daily standup updates using AI

[![Make.com](https://img.shields.io/badge/Make.com-6D00CC?style=flat&logo=make&logoColor=white)](https://make.com)
[![Groq](https://img.shields.io/badge/Groq-FF6B35?style=flat&logoColor=white)](https://groq.com)
[![Google Forms](https://img.shields.io/badge/Google_Forms-7AB4F5?style=flat&logo=google&logoColor=white)](https://forms.google.com)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)](https://sheets.google.com)
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white)](https://gmail.com)

---

## 🚨 Problem Statement

Agile teams waste 10–15 minutes every day manually collecting standup updates, formatting them, and sharing via email or chat. When team members are in different time zones, this becomes even harder — updates arrive at different times, some are missed, and the PM spends time chasing responses.

**This automation eliminates that entirely.**

---

## ✅ Solution

Team members submit their standup via a **Google Form**. The automation picks up all responses, sends them to **Groq AI** for summarisation, and delivers a clean, structured summary to the team via **Gmail** — all without any manual effort.

---

## 🔁 Workflow

```
Google Forms (Team submits standup)
        ↓
Google Sheets (Responses stored + deduplication check)
        ↓
Text Aggregator (Combine all entries into one block)
        ↓
Set Variable — cleanText (Sanitise aggregated content)
        ↓
HTTP Module → Groq API (AI summarisation)
        ↓
Gmail (Send formatted summary to team)
        ↓
Google Sheets (Mark entries as Processed)
```

---

## 🧩 Module Breakdown

| # | Module | Purpose |
|---|---|---|
| 1 | Google Sheets — Search Rows | Fetch unprocessed standup entries |
| 2 | Text Aggregator | Combine all responses into one text block |
| 3 | Set Variable (cleanText) | Sanitise and prepare text for AI |
| 4 | HTTP — Groq API | Send to LLM for summarisation |
| 5 | Gmail — Send Email | Deliver formatted summary |
| 6 | Google Sheets — Update Row | Mark entries as Processed |

---

## 🤖 AI Prompt Used

```
You are an agile team assistant. Below are daily standup updates from team members.

Summarise them clearly under three sections:
- ✅ What was done yesterday
- 🔨 What is planned for today
- 🚨 Blockers (if any)

Attribute each point to the respective team member.
Keep it concise and professional.

Standup Updates:
{{cleanText}}
```

---

## 📥 Google Form Fields

| Field | Type |
|---|---|
| Team Member Name | Short answer |
| What did you do yesterday? | Paragraph |
| What will you do today? | Paragraph |
| Any blockers? | Paragraph |

---

## 🗂️ Google Sheet Structure

| Column | Purpose |
|---|---|
| Timestamp | Auto-filled by Forms |
| Name | Team member name |
| Yesterday | Yesterday's update |
| Today | Today's plan |
| Blockers | Any blockers |
| Processed | ✅ Deduplication flag |

---

## ⚙️ Technical Notes

- **Deduplication:** `Processed` column prevents re-summarising already-handled entries
- **Trigger:** Scheduled (daily at standup time) or manual run
- **Groq Model:** `llama-3.3-70b-versatile` (free tier)
- **Temperature:** 0.3 (consistent, professional output)

---

## 💡 Consulting Insight

> This automation is typically the **entry point** for teams new to AI workflow automation. It delivers immediate, visible value on Day 1 — zero manual effort, clean output, and the team sees the AI in action. Estimated time saving: **1–2 hours/week** for a team of 5.

---

## 📸 Screenshots

*(Coming soon — Make.com scenario blueprint screenshot)*

---

*Part of the [Make.com Automation Suite](../README.md) | [Back to Portfolio](../../README.md)*
