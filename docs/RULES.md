# Development Rules
### QuickVoice — Engineering Standards and Collaboration Guidelines

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=12,20,26&height=8&section=header&width=100%" width="100%" />
</div>

This document defines the development rules, coding standards, and best practices to be followed across the **QuickVoice** monorepo. These guidelines ensure architectural modularity, real-time audio stability, strict type safety, and clean engineering collaboration between human developers and AI coding agents.

---

### <span style="background-color: #4F46E5; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">1</span> General Principles
*These rules apply across all applications and packages.*

<div style="background-color: #0D1117; border-left: 4px solid #4F46E5; border-radius: 6px; padding: 16px 20px; margin: 12px 0;">
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <b>Follow the project documentation</b> (<code>PRD.md</code>, <code>ARCHITECTURE.md</code>, <code>DESIGN.md</code>) before implementing new features.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <b>Maintain monorepo package boundaries.</b> Do not cross-import code between <code>apps/</code> without placing shared logic in <code>packages/</code>.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <b>Prioritize audio pipeline latency.</b> Never block the event loop or real-time audio frame loops with synchronous I/O.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <b>Make atomic, well-typed commits</b> that keep tests, linting, and build scripts green.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <b>Never expose secrets or telephony credentials</b> in code, commit history, or client bundles.</p>
</div>

---

### <span style="background-color: #4F46E5; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">2</span> Technology & Coding Standards
*Rules related to core languages, frameworks, and tools:*

| Category | Standard & Directive |
| :-- | :-- |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">TypeScript</span> | Use **TypeScript 5.x** with `strict: true`. Avoid using `any`; define explicit interfaces for all API payloads and telephony events. |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">Node.js / Express</span> | Use **Node.js 20 LTS**; wrap all asynchronous route handlers with centralized error middleware. |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">Python AI Worker</span> | Use **Python 3.12** matching CI; use `asyncio` for all LiveKit WebRTC event listeners and audio streaming tracks. |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">Database & ORM</span> | Use **Prisma ORM**; always generate migrations via `pnpm --filter @quickvoice/db migrate:dev` before deploying schema changes. |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">Package Manager</span> | Use **pnpm v9** with frozen lockfile (`pnpm-lock.yaml`). Never use `npm` or `yarn` in this monorepo. |
| <span style="background-color: #1E1B4B; color: #A5B4FC; border: 1px solid #4F46E5; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600;">Formatting & Lint</span> | Run **Prettier** and **ESLint** before staging; ensure zero syntax warnings in CI checks. |

---

### <span style="background-color: #4F46E5; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">3</span> Monorepo Directory Boundaries
*Follow defined architectural domains in <code>ARCHITECTURE.md</code>:*

<div style="background-color: #0D1117; border-left: 4px solid #4F46E5; border-radius: 6px; padding: 16px 20px; margin: 12px 0;">
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <code>apps/console</code> and <code>apps/web</code> are pure Next.js web applications; they interact with backend logic strictly via HTTP/WSS API.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <code>apps/server</code> handles authentication, billing, call dispatch, campaign scheduling, and database access.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <code>apps/ai</code> handles real-time WebRTC audio streams, VAD, STT, LLM streaming, and TTS synthesis.</p>
  <p style="margin: 6px 0; color: #F0F6FC;">&bull; <code>packages/db</code> owns the canonical database schema and Prisma client distribution.</p>
</div>

---

### <span style="background-color: #4F46E5; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">4</span> Real-Time Audio & Telephony Performance Guidelines

* **Latency Ceilings**: Maintain time-to-first-token (TTFT) audio delivery $< 500$ ms. Stream clause boundaries immediately rather than waiting for complete sentences.
* **Barge-In Sensitivity**: Ensure Silero VAD is tuned with a minimum threshold of $0.5$ to prevent background noise from interrupting speech while maintaining instant interruption responsiveness.
* **Audio Buffer Cleanup**: Clear internal TTS playback queues immediately when a barge-in event is detected to prevent overlapping audio frames.
* **Telephony Webhook Verification**: Always validate Twilio / Telnyx cryptographic signatures before accepting incoming SIP dispatches.

---

### <span style="background-color: #4F46E5; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">5</span> AI Collaboration Guidelines (Cursor & Agent Rules)

* **Read `MEMORY.md` First**: Always check active phase, completed tasks, and architectural decisions before writing code.
* **Preserve Monorepo Integrity**: Run `pnpm turbo build` to verify cross-package contracts before completing edits.
* **Update Documentation**: Keep `TASKS.md` and `MEMORY.md` synchronized whenever modifying agent features or API schemas.

---

### <span style="background-color: #EA4335; color: white; padding: 2px 8px; border-radius: 4px; font-weight: 700; font-size: 12px; margin-right: 6px;">6</span> Prohibited Patterns

* **Do not** commit raw API keys (OpenAI, Deepgram, Twilio, Telnyx, LiveKit) into repository files or git history.
* **Do not** use blocking synchronous functions (`time.sleep()`, `fs.readFileSync()`) inside real-time audio or WebSocket event loops.
* **Do not** store raw audio recordings in unencrypted local storage; always upload through authorized cloud buckets.
* **Do not** bypass Prisma migrations by directly modifying live database schemas.