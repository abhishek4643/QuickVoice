<div align="center">

# 🎙️ QuickVoice

### **Open-Source Platform for Building & Operating AI Phone Agents**

_Build intelligent voice assistants that handle real phone calls autonomously_

[![Live Platform](https://img.shields.io/badge/🌐_Platform-quickvoice.co-0A66C2?style=for-the-badge)](https://quickvoice.co)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue?style=for-the-badge)](https://www.gnu.org/licenses/agpl-3.0)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)

</div>

---

## 📌 About

QuickVoice is a **self-hostable**, open-source platform for creating and managing AI-powered phone agents. It enables businesses to automate phone interactions — from customer support to appointment booking — using cutting-edge conversational AI.

> _Forked from [allgpt-co/QuickVoice](https://github.com/allgpt-co/QuickVoice) to explore, customize, and contribute to the growing AI voice ecosystem._

---

## 🧠 What Makes QuickVoice Powerful

| Capability | Description |
|-----------|-------------|
| 📞 **Inbound & Outbound Calls** | Handle incoming calls and initiate outgoing campaigns |
| 🤖 **AI-Driven Conversations** | Natural language understanding with LLM-powered responses |
| 🔄 **Real-Time Processing** | Sub-second latency via LiveKit WebRTC infrastructure |
| 🛠️ **Fully Customizable** | Define custom prompts, workflows, and tool integrations |
| 📊 **Call Analytics** | Track call duration, sentiment, outcomes, and transcripts |
| 🔌 **Telephony Integrations** | Native support for Twilio, Telnyx, and more |
| 🏠 **Self-Hostable** | Deploy on your own infrastructure for full data control |

---

## 🛠️ Tech Stack

```
Frontend:       Next.js · TypeScript · React
Backend:        FastAPI (Python) · Express.js (Node)
Real-Time:      LiveKit (WebRTC)
Database:       PostgreSQL
Telephony:      Twilio · Telnyx
AI/ML:          OpenAI GPT · Custom LLM Integration
Orchestration:  Docker · Docker Compose
Protocol:       MCP (Model Context Protocol)
```

---

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- API keys for Twilio/Telnyx and OpenAI

### Deploy with Docker

```bash
# Clone the repository
git clone https://github.com/abhishek4643/QuickVoice.git
cd QuickVoice

# Configure environment variables
cp .env.example .env
# Edit .env with your API keys

# Launch all services
docker-compose up -d
```

Access the dashboard at [http://localhost:3000](http://localhost:3000)

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────┐
│              QuickVoice Platform             │
├──────────┬──────────────┬───────────────────┤
│  Next.js │   FastAPI    │     LiveKit       │
│   UI     │   Backend    │   Voice Engine    │
├──────────┴──────────────┴───────────────────┤
│              PostgreSQL Database             │
├─────────────────────────────────────────────┤
│       Twilio / Telnyx Telephony Layer       │
└─────────────────────────────────────────────┘
```

---

## 🤝 Use Cases

- **Customer Support Automation** — Handle FAQs, ticket creation, and escalations
- **Appointment Scheduling** — Book, confirm, and reschedule appointments by phone
- **Lead Qualification** — Screen and qualify sales leads autonomously
- **Survey & Feedback Collection** — Conduct phone surveys at scale
- **Order Status & Tracking** — Provide real-time order updates via voice

---

## 📄 License

This project is licensed under the **GNU Affero General Public License v3.0** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

_Empowering businesses with intelligent voice automation_ 🎙️

</div>
