# Project Memory
### QuickVoice — Engineering Context, Operational State, and Architectural History

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=12,20,26&height=8&section=header&width=100%" width="100%" />
</div>

This document maintains operational context, key architectural decisions, and runtime constraints to ensure continuity across development sessions, automated agent workflows, and human contributors.

---

### Current Phase: Phase 5 — Production Release
* **Last Updated**: October 31, 2026
* **Status**: Complete &amp; Benchmark Verified (Sub-450ms Conversational Latency)

### High-Level Checklist
- [x] Phase 1: LiveKit WebRTC Core &amp; Audio Pipeline
- [x] Phase 2: Speech Intelligence &amp; Barge-In Engine
- [x] Phase 3: Telephony Gateway &amp; SIP Trunking
- [x] Phase 4: Customer Console &amp; REST API Server
- [x] Phase 5: Verification, Analytics &amp; Production Monorepo Delivery

---

### Current Status

<div style="background-color: #0D1117; border-left: 4px solid #10B981; border-radius: 6px; padding: 16px 20px; margin: 12px 0;">
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>LiveKit Python Audio Worker Operational</b> (bi-directional WebRTC room management in <code>apps/ai</code>).</p>
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>Real-Time Speech Stack Integrated</b> (Silero VAD + Deepgram Nova-2 STT + Cartesia Sonic TTS).</p>
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>Conversational Barge-In Verified</b> (TTS queues dynamically flushed upon user voice interruption).</p>
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>Customer Console &amp; Express API Active</b> (agent prompt tuning, analytics, and call logs in <code>apps/console</code>).</p>
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>Prisma Schema &amp; PostgreSQL Persisted</b> (call sessions, transcripts, campaigns, and audio metrics in <code>packages/db</code>).</p>
  <p style="margin: 6px 0; color: #F0F6FC;">[x] <b>Production Documentation Suite Active</b> (aligned with visual UI standard across all 6 files).</p>
</div>

---

### Completed Milestones

| ID | Milestone Description | Completed Date |
| :-: | :-- | :-: |
| **1.1** | Setup Turborepo workspace, pnpm lockfile, and shared TypeScript configurations | Aug 14, 2026 |
| **1.2** | Build LiveKit WebRTC audio worker loop with Silero VAD frame processor | Aug 28, 2026 |
| **1.3** | Implement streaming speech-to-speech pipeline with Deepgram and Cartesia Sonic | Sep 12, 2026 |
| **1.4** | Integrate Twilio and Telnyx SIP trunking for cellular phone dispatch | Sep 26, 2026 |
| **1.5** | Develop Next.js customer console for prompt management and call audio scrubber | Oct 10, 2026 |
| **1.6** | Publish complete architectural documentation suite in `docs/` | Oct 31, 2026 |

---

### Key Architectural Decisions Log

* **ADR-001: WebRTC Streaming via LiveKit over Raw WebSockets**: LiveKit handles packet loss concealment, audio frame synchronization, and NAT traversal out-of-the-box, ensuring conversational audio never degrades under high network jitter.
* **ADR-002: Clause-Boundary LLM Streaming to TTS**: Instead of waiting for full LLM responses or sentences, text tokens are chunked at natural punctuation marks and sent directly to Cartesia TTS, cutting conversational turnaround to under 450ms.
* **ADR-003: Redis BullMQ Outbound Telephony Dispatch**: Queueing outbound calls through Redis ensures cellular rate limits from carriers (Twilio / Telnyx) are strictly respected without dropping concurrent calls.

---

### Operational Constraints & Guardrails

1. **Carrier Rate Limits**: Twilio and Telnyx enforce strict concurrent call limits per SIP trunk. Outbound campaigns must be throttled via BullMQ rate-limiting settings.
2. **Audio Stream Memory Leakage**: When telephone calls disconnect abruptly, active WebRTC room handles and TTS buffer subscriptions must be immediately disposed of to avoid VRAM/RAM accumulation.
3. **Sensitive Audio Data (PII)**: Transcripts containing sensitive customer payment or medical data must be encrypted at rest in PostgreSQL with restricted console access.