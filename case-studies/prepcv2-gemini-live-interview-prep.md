# PrepCV2 Gemini Live Interview Prep

## Summary

An AI interview-prep SaaS with Gemini Live voice interviews, resume-aware prompts, coding tracks, proctoring signals, structured reports, credit purchases, object storage, and VLSI-specific Verilog practice.

## My Role

Full-stack AI interview product engineering across realtime interview sessions, assessment flows, billing state, proctoring, reports, and technical practice modules.

## Problem

Interview preparation is fragmented. Voice interviews, coding practice, resumes, payments, reports, and proctoring often exist as separate tools. PrepCV2 combines them into one SaaS workflow.

The system needs to handle:

- Realtime AI interviews
- Resume-aware prompts
- Technical practice across multiple domains
- Attempt and report tracking
- Payment idempotency and credit accounting
- Proctoring signals
- File storage for resume/artifact context
- VLSI-specific Verilog workflows

## Product Scope

- Gemini Live realtime voice interview sessions
- Resume-aware interview prompts
- DSA, React, VLSI, SQL, and ML interview tracks
- Proctoring signals and violation tracking
- Structured post-interview reports
- Razorpay credit purchases and webhook processing
- Convex backend state for attempts, reports, billing, and users
- Cloudflare R2 storage for resumes and artifacts
- VLSI Verilog practice with synthesis/simulation feedback

## Engineering Highlights

- Built realtime interview orchestration around Gemini Live and Vertex-style bidirectional sessions.
- Added proctoring-oriented signals including fullscreen/violation tracking patterns.
- Implemented Razorpay webhook processing with multi-secret validation and event persistence.
- Used authoritative purchase selection and status-priority logic to avoid duplicate or incorrect credit fulfillment.
- Added a 2-hour reconciliation cron for stale Razorpay credit purchases.
- Enabled React Compiler in the production Next.js app.
- Built a VLSI Verilog flow with Monaco editor support, Yosys WASM synthesis, DigitalJS circuits, and simulation checks.

## Architecture

```text
Next.js Interview App
        |
        +--> Gemini Live / Vertex-style realtime voice session
        |
        +--> Coding and VLSI practice modules
        |       |
        |       v
        |    Monaco + Yosys WASM + DigitalJS simulation
        |
        +--> Convex backend
        |       |
        |       v
        |    attempts, reports, billing state, webhook events
        |
        +--> Razorpay webhooks + 2-hour reconciliation cron
        |
        +--> R2 object storage for resumes/artifacts
```

## Key Tradeoffs

- Payment fulfillment must be idempotent because webhooks can arrive more than once, in different orders, or after checkout state changes.
- Realtime interview state and post-interview reports need durable backend records so the user journey survives reloads or failures.
- VLSI coding practice needs domain-specific tooling; generic code editors are not enough for Verilog synthesis and circuit-level validation.

## Tech Stack

- Next.js
- React
- TypeScript
- Gemini Live
- Vertex AI style realtime sessions
- Convex
- Razorpay
- Cloudflare R2
- Yosys WASM
- DigitalJS
- Monaco Editor
- React Compiler
- WebSockets
- Tailwind CSS

## What I Learned

- Realtime AI products need reliable product accounting around attempts, credits, and reports.
- Payment correctness is a backend systems problem, not a checkout UI problem.
- Specialized technical interview tracks become much stronger when they use domain-specific evaluation tools.
