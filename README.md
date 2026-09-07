# QuickVoice

An open-source operating platform for building, deploying, and managing autonomous AI phone agents capable of natural, sub-second latency voice conversations over standard telephony networks.

[![Platform](https://img.shields.io/badge/Platform-quickvoice.co-0A66C2?style=for-the-badge)](https://quickvoice.co)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/License-AGPL_v3-blue?style=for-the-badge)](https://www.gnu.org/licenses/agpl-3.0)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![WebRTC](https://img.shields.io/badge/WebRTC-LiveKit-FF6B6B?style=for-the-badge)](https://livekit.io/)

---

## Project Overview

QuickVoice provides production-grade infrastructure for orchestrating voice-based artificial intelligence. Traditional voice bots suffer from unnatural delays and rigid decision trees. QuickVoice solves this by integrating WebRTC audio streaming, streaming speech-to-text, large language model decision engines, and expressive speech synthesis into a sub-500ms conversational loop.

**Vision:** Democratize enterprise-grade conversational AI by providing a developer-first platform that connects any LLM to real-world phone lines with full operational control.

---

## Live Platform

Experience the platform documentation and dashboard:
- **Platform URL:** [https://quickvoice.co](https://quickvoice.co)
- **Deployment Status:** Active Production Platform
- **Deployment Model:** Cloud Hosted & Self-Hostable via Docker

---

## Key Features

- **Bidirectional Telephony Integration:** Seamless connectivity with Twilio, Telnyx, and SIP trunks for inbound and outbound calling.
- **Sub-Second Audio Pipeline:** Low-latency WebRTC audio transport powered by LiveKit for interruption-friendly conversations.
- **Model Context Protocol (MCP) Integration:** Extensible tool execution allowing voice agents to query databases and trigger APIs mid-call.
- **Comprehensive Agent Dashboard:** Real-time call monitoring, latency breakdown, full audio transcripts, and sentiment tracking.
- **Multi-Tenant Architecture:** Granular workspace management with role-based access control and telephony credential isolation.
- **Self-Hostable Deployment:** Complete Docker and Docker Compose definitions for private cloud or on-premise execution.

---

## Use Cases

### For Contact Centers & Enterprise Support
- Automate high-frequency customer inquiries and status checks without human queueing.
- Perform intelligent routing with context passed directly to human agents when escalation occurs.

### For Appointment-Based Healthcare & Services
- Conduct automated confirmation calls, intake questionnaires, and calendar rescheduling.
- Send proactive reminders with real-time conversational answers to client questions.

### For Developers & Platform Engineers
- Prototype customized voice agents with distinct system instructions, knowledge bases, and function hooks.
- Inspect detailed audio packet telemetry and token generation times for performance tuning.

---

## System Architecture

```
+---------------+       SIP / WebRTC       +-------------------------+
| Caller / PSTN | <======================> | Telephony Gateway       |
+---------------+                          | (Twilio / Telnyx)       |
                                           +-------------------------+
                                                        |
                                                  Audio Stream
                                                        v
+------------------+     LiveKit WebRTC     +-------------------------+
| Voice Agent Core | <===================> | Media Server (LiveKit)  |
|  - STT Pipeline  |                       +-------------------------+
|  - LLM Decision  |                                    |
|  - TTS Engine    | <--- MCP Tool Calls ---> [ Enterprise APIs / DB ]
+------------------+
```

---

## Technology Stack

| Layer | Technologies |
|---|---|
| Dashboard Frontend | Next.js, React, TypeScript, Tailwind CSS |
| Real-Time Media Engine | LiveKit WebRTC Infrastructure |
| Telephony Providers | Twilio Voice, Telnyx SIP Trunking |
| Protocol Standard | Model Context Protocol (MCP) |
| Containerization | Docker, Docker Compose |
| Package Monorepo | Turborepo / Yarn Workspaces |

---

## Project Structure

```
QuickVoice/
├── apps/                 # Application entrypoints
│   ├── web/              # Management dashboard and configuration portal
│   └── agent-server/     # Voice agent runner and WebRTC session controller
├── packages/             # Shared packages and internal libraries
│   ├── core/             # Business logic and session lifecycle handlers
│   ├── telephony/        # Twilio and Telnyx telephony adapters
│   └── mcp-tools/        # Model Context Protocol tool integrations
├── docs/                 # Platform guides and API specifications
├── scripts/              # Build, migration, and deployment utilities
├── security/             # Security policy and disclosure documentation
└── docker-compose.yml    # Container composition for local execution
```

---

## Getting Started

### Prerequisites
- Docker Engine >= 24.0 and Docker Compose >= 2.20
- Node.js >= 18.0.0
- Twilio or Telnyx telephony account credentials

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/abhishek4643/QuickVoice.git
   cd QuickVoice
   ```

2. Configure environment variables:
   ```bash
   cp .env.example .env
   ```
   Populate your `.env` file with your LiveKit and telephony API keys.

3. Start services via Docker Compose:
   ```bash
   docker compose up -d
   ```

4. Access the web dashboard at `http://localhost:3000`

---

## Future Roadmap

- Advanced voice cloning and custom acoustic model fine-tuning.
- Multi-party conference calling with autonomous AI moderation.
- Outbound campaign scheduler with predictive dialing logic.
- Expanded native CRM integrations for Salesforce and HubSpot.

---

## License

This project is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0).
