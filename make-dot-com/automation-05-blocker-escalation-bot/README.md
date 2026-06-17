# 🚨 Automation #05 — Blocker Escalation Bot
### Automatically detect, classify, and escalate team blockers via Slack and Gmail using AI

[![Make.com](https://img.shields.io/badge/Make.com-6D00CC?style=flat&logo=make&logoColor=white)](https://make.com)
[![Groq](https://img.shields.io/badge/Groq-FF6B35?style=flat&logoColor=white)](https://groq.com)
[![Slack](https://img.shields.io/badge/Slack-4A154B?style=flat&logo=slack&logoColor=white)](https://slack.com)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)](https://sheets.google.com)
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white)](https://gmail.com)

---

## 🚨 Problem Statement

Blockers reported in standups often sit unresolved for days because there is no formal escalation path. PMs manually track blockers across standup notes, Slack messages, and spreadsheets — and by the time the right person is notified, delivery has already slipped. There is no automated triage, no priority classification, and no audit trail.

**This automation detects blockers, classifies their severity, and escalates them to the right channel instantly — without the PM manually intervening.**

---

## ✅ Solution

When a blocker is submitted (via Google Sheets from standup data), the automation sends it to **Groq AI** for severity classification and recommended action. Based on the classification, it routes the escalation to **Slack** (for real-time team visibility) and **Gmail** (for formal stakeholder notification) — with a full audit log maintained in Google Sheets.

---

## 🔁 Workflow

```
Google Sheets (Blocker detected from standup data)
        ↓
Text Aggregator (Prepare blocker details)
        ↓
HTTP Module → Groq API (Classify severity + recommended action)
        ↓
Google Sheets — Get a Row (Re-expose variables)
        ↓
Router (Branch by severity: Critical / High / Medium)
        ↓
    ┌───────────────────┬──────────────────────┐
    ↓                   ↓                      ↓
Slack Alert         Gmail — PM Notice      Google Sheets
(Critical/High)     (Critical only)        (Log all blockers)
        ↓                   ↓
Google Sheets       Google Sheets
(Update status)     (Update status)
```

---

## 🧩 Module Breakdown

| # | Module | Purpose |
|---|---|---|
| 1 | Google Sheets — Search Rows | Detect unprocessed blocker entries |
| 2 | Iterator | Loop through each blocker |
| 3 | Text Aggregator | Prepare blocker text for AI |
| 4 | Set Variable (cleanText) | Sanitise input |
| 5 | HTTP — Groq API | Classify severity + recommend action |
| 6 | Google Sheets — Get a Row | Re-expose AI response variables |
| 7 | Router | Branch logic by severity level |
| 8 | Slack — Post Message (Critical) | Immediate Slack alert for critical blockers |
| 9 | Slack — Post Message (High) | Slack alert for high priority blockers |
| 10 | Gmail — Send Email (Critical) | Formal escalation email to stakeholders |
| 11 | Google Sheets — Update Row | Log severity + escalation status |
| 12–21 | Filters + Aggregators + Error handlers | Conditional logic, data mapping, resilience |

---

## 🤖 AI Prompt Used

```
You are an agile delivery assistant specialising in risk and blocker management.

Analyse the blocker below and respond with:
1. Severity: Critical / High / Medium / Low
2. Category: Technical / Resource / Dependency / Process / External
3. Recommended Action: A concise next step for the PM to resolve this blocker
4. Escalation needed: Yes / No

Be direct and concise. Format your response exactly as:
Severity: [level]
Category: [type]
Recommended Action: [action]
Escalation needed: [Yes/No]

Blocker Details:
{{cleanText}}
```

---

## 📥 Input Data Structure (Google Sheets)

| Column | Purpose |
|---|---|
| Timestamp | When blocker was reported |
| Reporter | Team member who raised it |
| Blocker Description | Full blocker details |
| Affected Task / Story | What is being blocked |
| Days Blocked | How long it has been unresolved |
| Processed | Deduplication flag |

---

## 🗂️ Escalation Log Sheet

| Column | Purpose |
|---|---|
| Timestamp | When escalation was triggered |
| Reporter | Who raised the blocker |
| Blocker | Description |
| Severity | AI classification |
| Category | Blocker type |
| Recommended Action | AI-suggested next step |
| Escalation Sent | Slack / Gmail / Both |
| Status | Open / In Progress / Resolved |

---

## 📣 Slack Message Format

```
🚨 *BLOCKER ESCALATION ALERT*

*Reporter:* John
*Severity:* 🔴 Critical
*Category:* Dependency

*Blocker:*
Payment gateway API credentials not provided by client.
Sprint delivery at risk.

*Recommended Action:*
Escalate to client account manager immediately.
Request credentials or workaround by EOD.

*Days Blocked:* 3
*Logged:* 17 Jun 2026
```

---

## 📧 Gmail Escalation Format

```
Subject: 🚨 Critical Blocker — Immediate Attention Required | [Project Name]

A critical blocker has been detected and requires your immediate attention.

Reporter: John
Blocker: Payment gateway API credentials not provided by client
Severity: Critical
Category: Dependency
Days Blocked: 3

Recommended Action:
Escalate to client account manager immediately.
Request credentials or workaround by EOD.

This has been logged in the project tracker.
Please action within 24 hours to avoid sprint delivery impact.
```

---

## ⚙️ Technical Notes

- **Trigger:** Scheduled scan (every morning) or manual run
- **Modules:** 21+ (most complex automation in the portfolio)
- **Routing Logic:** Router branches on AI-classified severity level
- **Key Workaround:** `Google Sheets → Get a Row` after Groq response to re-expose variables
- **Groq Model:** `llama-3.3-70b-versatile`
- **Temperature:** 0.1 (very low — precise classification required)
- **API Response Path:** `data → choices → [] → message → content`
- **Resilience:** Error handler modules added to prevent scenario failure on API timeout

---

## 💡 Consulting Insight

> Blocker escalation is where delivery teams lose the most time — not because blockers are hard to solve, but because the right person doesn't know about them fast enough. This automation closes that gap with AI-powered triage and multi-channel escalation. It also creates a searchable blocker history that reveals recurring patterns — a goldmine for agile coaching and process improvement. Estimated impact: **prevents 1–3 days of delivery slip per sprint** in teams of 5–10.

---

## 📸 Screenshots

*(Coming soon — Make.com scenario blueprint screenshot)*

---

*Part of the [Make.com Automation Suite](../README.md) | [Back to Portfolio](../../README.md)*
