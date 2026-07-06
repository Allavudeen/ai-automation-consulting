# 🏥 n8n #04 — AI-Powered Appointment & Sales Agent (MCP + RAG Architecture)

An end-to-end conversational AI agent built on n8n using Model Context Protocol (MCP) and RAG-style data querying. Handles full appointment lifecycle — booking, rescheduling, and cancellation — plus real-time sales register lookup and general web search, all via a single mobile-responsive chat UI.

Google Calendar is the single source of truth. Google Sheets serves as both a write-only appointment audit log and a RAG-queryable sales data source.

---

## 🛠 Tech Stack

![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Groq](https://img.shields.io/badge/Groq_LLM-F55036?style=for-the-badge&logo=groq&logoColor=white)
![Google Calendar](https://img.shields.io/badge/Google_Calendar-4285F4?style=for-the-badge&logo=googlecalendar&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)
![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)
![SerpApi](https://img.shields.io/badge/SerpApi-00AC47?style=for-the-badge&logo=google&logoColor=white)
![MCP](https://img.shields.io/badge/MCP_Architecture-6C47FF?style=for-the-badge&logo=anthropic&logoColor=white)
![RAG](https://img.shields.io/badge/RAG_on_Sheets-FF6B35?style=for-the-badge&logo=databricks&logoColor=white)
![HTML](https://img.shields.io/badge/Chat_UI-E34F26?style=for-the-badge&logo=html5&logoColor=white)

---

## 🧠 Architecture Overview

```
User (Chat UI)
      │
      ▼
n8n AI Agent (Groq LLM)
      │
      ├── MCP Tools
      │     ├── Google Calendar  ← Book / Reschedule / Cancel events
      │     ├── Google Sheets    ← Appointment audit log + Sales RAG source
      │     └── Gmail            ← Confirmation & cancellation emails
      │
      ├── SerpApi               ← General web search queries
      │
      └── RAG Layer
            └── Sheets query    ← Sales register lookup (transaction & amount)
```

---

## ✅ Features

### 📅 Appointment Management (MCP)
- **Book** — Collects Name, Email, Mobile, Symptom, Doctor; checks slot availability; creates Calendar event; logs to Sheets; sends Gmail confirmation
- **Reschedule** — Fetches live EventID from Calendar; verifies new slot availability; updates Calendar + Sheets + Gmail
- **Cancel** — Fetches appointments by email; confirms with user; deletes from Calendar; logs cancellation timestamp; sends Gmail notification

### 📊 Sales Register Lookup (RAG)
- Query Google Sheets sales data conversationally
- Look up highest transactions, amounts by date, sales by party/category
- RAG-style retrieval — agent reads and reasons over Sheets rows in real time

### 🔎 General Web Search (SerpApi)
- Answer any question outside appointments and sales
- Live web search via SerpApi integrated directly into the same chat

---

## 🗂 Key Design Decisions

| Decision | Rationale |
|---|---|
| Google Calendar = Source of Truth | All reschedule/cancel ops fetch live EventID from Calendar, never from Sheets |
| Sheets = Dual Role | Write-only audit log for appointments AND RAG data source for sales queries |
| MCP Architecture | Clean tool routing; agent decides which tool to call based on user intent |
| RAG on Sheets | No vector DB needed; agent retrieves and reasons over structured sales rows directly |
| ISO 8601 + IST | All Calendar API calls use `YYYY-MM-DDTHH:MM:SS+05:30`; display uses 12-hour AM/PM |
| Cancellation timestamp | `new_datetime` on cancel records the exact time of cancellation for audit trail |
| `$fromAI()` expressions | Single-line only; no line breaks inside `{{ }}` |

---

## 📁 Folder Structure

```
n8n/
└── automation-04-appointment-management-agent/
    ├── workflow.json        ← Sanitized n8n workflow export
    ├── index.html           ← Mobile-responsive chat UI
    ├── screenshots/         ← Demo screenshots
    └── README.md
```

---

## 📸 Screenshots

### 🌐 Chat UI — General Web Search
> Ask anything via SerpApi — live web search directly in the chat

![Chat General Search](screenshots/01-chat-general.jpg)

---

### 📊 Sales Register — Google Sheets Data Source
> Structured sales data in Sheets used as RAG source for conversational queries

![Sales Register Sheet](screenshots/02-sales-register.jpg)

---

### 💬 Chat UI — Sales Register Query (RAG)
> "What is the highest debit and credit transaction?" — answered from Sheets in real time

![Chat Sales Query](screenshots/03-chat-sales-register-details.jpg)

---

### 📅 Chat UI — New Appointment Booking
> Agent collects patient details, confirms slot, books appointment end-to-end

![Chat Booking](screenshots/04-chat-apmt-new-booking.jpg)

---

### 🗓 Google Calendar — Appointment Created
> Full patient context (Name, Email, Mobile, Symptom, Doctor) stored in every event

![Google Calendar](screenshots/05-google-calendar-appointment.jpg)

---

### 📋 Google Sheets — Appointment Audit Log
> Every booking, reschedule, and cancellation timestamped and tracked

![Google Sheets Log](screenshots/06-google-sheet-log.jpg)

---

### 📧 Gmail — Confirmation Email
> Automatic confirmation email sent to patient immediately after booking

![Gmail Confirmation](screenshots/07-google-gmail.jpg)

---

## 🔗 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/allavudeen)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Allavudeen/ai-automation-consulting)
[![Upwork](https://img.shields.io/badge/Upwork-6FDA44?style=for-the-badge&logo=upwork&logoColor=white)](https://www.upwork.com)

