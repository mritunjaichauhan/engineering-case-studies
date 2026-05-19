# PrepViva Realtime Voice Interviews

## Summary

A UK-focused realtime AI interview simulator for Medical MMI, NHS, postgraduate, admissions, technical, and business-style interview practice.

The product uses realtime speech instead of a text-only chat interface and supports station-style practice, final reports, authentication, paid access, and product analytics.

## My Role

Realtime AI interview and product engineering across browser voice sessions, Amazon Nova Sonic relay integration, session lifecycle handling, reconnect behavior, and interview UX.

## Public-Safe Evidence Notes

- Timeframe: 2025 realtime AI product work.
- Evidence type: sanitized voice-session lifecycle notes, reconnect strategy, UX constraints, and product architecture.
- My contribution: implementation across browser voice sessions, relay integration, reconnect behavior, continuation prompts, and interview UX.
- Not included: private source code, production prompts, user conversations, customer data, or provider credentials.

## Problem

High-stakes interviews are spoken, timed, and context-dependent. A useful simulator needs to preserve the feeling of a real interview while handling practical realtime-AI constraints:

- Realtime speech input/output
- Turn-taking and barge-in behavior
- Session limits and token expiry
- Continuity across reconnects
- Interview-specific prompting
- Final reports and measurable outcomes

## Product Scope

- Realtime AI interviewer
- Medical MMI and NHS interview workflows
- Postgraduate/admissions interview flows
- Station circuits and final performance reports
- Passkeys and Google sign-in
- KV-backed sessions
- Paid access and billing boundaries
- PostHog analytics

## Engineering Highlights

- Integrated browser voice sessions with an Amazon Nova Sonic relay.
- Added proactive hot-swap reconnects before provider session limits using soft and hard safety thresholds.
- Preserved conversation history across reconnects so the AI interviewer does not repeat introductions or restart the scenario.
- Added continuation prompts with explicit rules such as not re-introducing itself after reconnect.
- Included token refresh before reconnect because realtime session tokens expire.
- Used silence-aware swapping when possible and forced swapping when necessary.
- Added watchdog logging after reconnects to detect silent or stalled sessions.

## Architecture

```text
Browser Interview UI
        |
        v
Amazon Nova Sonic client state
        |
        v
Relay server
        |
        v
Amazon Nova Sonic realtime session

Reconnect path:
timer -> wait for silence if possible -> close old session -> refresh token -> replay history -> continue interview
```

## Key Tradeoffs

- Waiting for silence creates a smoother handoff, but a hard deadline is still needed to avoid hitting upstream session limits.
- History replay is necessary for continuity, but prompts must explicitly prevent the model from treating reconnects like new interviews.
- Voice interview UX needs reliability work that users never notice when it works correctly.

## Tech Stack

- Next.js
- TypeScript
- Amazon Nova Sonic
- WebSockets
- Passkeys
- Google OAuth
- KV sessions
- Autumn billing
- PostHog
- Tailwind CSS

## What I Learned

- Realtime AI quality is as much about session orchestration as model choice.
- Voice products need lifecycle engineering: reconnects, token refresh, watchdogs, state replay, and interruption handling.
- Strong prompts are not enough unless the transport/session layer preserves context correctly.
