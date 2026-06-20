# n8n — AI Workflow Automation

This folder contains AI-powered workflows built with **n8n**, a self-hosted, open-source workflow automation platform. All workflows in this section run locally via Docker, with no cloud dependency for the orchestration layer.

---

## Why n8n

| Feature | Benefit |
|---|---|
| Self-hosted via Docker | Full control, no vendor lock-in |
| Open-source | Customizable, community-backed |
| AI Agent support | Native LangChain integration |
| 400+ integrations | Connect any tool or API |
| Persistent memory | Postgres-backed conversation history |
| Visual canvas | Easy to build, debug, and document |

n8n complements Make.com in this portfolio by enabling **agentic, conversational AI workflows** — where the AI reasons, decides, and acts — rather than fixed linear automation paths.

---

## Local Stack

All workflows in this folder run on the following local setup:

| Layer | Tool |
|---|---|
| Containerization | Docker (self-hosted) |
| Orchestration | n8n (latest) |
| Vector Store | Supabase (pgvector) |
| Conversation Memory | PostgreSQL |
| Embedding Model | HuggingFace Inference API |
| LLM | Google Gemini / Groq |

---

## Workflows

| # | Workflow | Description | Status |
|---|---|---|---|
| 01 | [Gmail AI Agent](./gmail-ai-agent/) | Conversational agent that sends emails via natural language instructions | ✅ Complete |
| 02 | [RAG Document Intelligence Agent](./rag-document-intelligence-agent/) | Upload any document once, query it conversationally forever using RAG + Supabase vector store | ✅ Complete |
| 03 | Sprint Planning Assistant | Conversational agent for sprint goal generation and capacity planning | 🔧 Planned |
| 04 | Standup Coach | Team members chat their update; agent formats and logs it | 🔧 Planned |
| 05 | Sprint Health Monitor | Monitors velocity and flags risks via weekly digest | 🔧 Planned |
| 06 | Burndown Alert Agent | Tracks remaining work vs days left; escalates if off-track | 🔧 Planned |

---

## Key Design Patterns

**Agentic Reasoning**
Unlike linear automation, n8n AI Agents decide which tools to call based on context. The agent reasons before acting — not just triggering a fixed sequence.

**Persistent Memory**
Postgres Chat Memory stores conversation history across sessions. Every interaction is logged, traceable, and auditable — critical for enterprise use cases.

**RAG Architecture**
Documents are chunked, embedded via HuggingFace, and stored as vectors in Supabase. The AI Agent retrieves the most relevant chunks at query time and synthesizes accurate answers.

**Tool-Agnostic Consulting**
These workflows demonstrate the same Agile automation concepts as the Make.com series — but using a different paradigm. The goal is always the same: reduce manual overhead for Agile teams.

---

## Portfolio Context

This n8n series is part of a broader **AI-Augmented Agile** consulting portfolio:

- **Make.com Series** → Structured, scheduled automations for Agile reporting
- **n8n Series** → Agentic, conversational AI workflows for Agile decision support

Together they demonstrate tool-agnostic AI automation expertise applied to real Agile and Scrum challenges.

🔗 Full portfolio: [github.com/Allavudeen/ai-automation-consulting](https://github.com/Allavudeen/ai-automation-consulting)

---

*All workflows are sanitized before publishing. Replace placeholder credential values before use. See individual workflow READMEs for setup instructions.*
