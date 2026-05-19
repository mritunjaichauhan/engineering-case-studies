# Engineering Case Studies

Sanitized engineering case studies from private production SaaS work. This repository does not include proprietary source code, secrets, customer data, internal URLs, or private business data.

I use this repo to make private work reviewable: architecture decisions, product constraints, system design, operational concerns, and the engineering problems behind the products.

## Focus Areas

- Campus placement and student management systems
- Realtime voice AI interviews
- AI resume and career SaaS
- Multi-tenant SaaS architecture
- Payments, credits, billing, and reconciliation
- RBAC, audit logs, rate limits, and abuse prevention
- Cloudflare Workers, Convex, Next.js, TypeScript, and edge-first product infrastructure

## Case Studies

| Case Study | What It Shows |
| --- | --- |
| [Campus Placement Management System](case-studies/campus-placement-management-system.md) | Multi-tenant placement workflows, RBAC, Convex data modeling, audit logs, rate limits, mobile/web/API architecture |
| [RebuildCV AI Resume SaaS](case-studies/rebuildcv-ai-resume-saas.md) | AI resume optimization, CareerGPT, Razorpay billing, Zoho invoices, D1 schema, Cloudflare AI Gateway |
| [PrepViva Realtime Voice Interviews](case-studies/prepviva-realtime-voice-interviews.md) | AWS Nova Sonic realtime voice UX, proactive hot-swap reconnects, history replay, paid interview sessions |
| [PrepCV2 Gemini Live Interview Prep](case-studies/prepcv2-gemini-live-interview-prep.md) | Gemini Live interviews, proctoring, payment idempotency, VLSI Verilog/Yosys flow, Convex backend |

## Architecture Notes

- [Campus Placement Architecture](diagrams/campus-placement-architecture.md)
- [Realtime Voice Hot-Swap](diagrams/realtime-voice-hot-swap.md)
- [Payment Reconciliation](diagrams/payment-reconciliation.md)

## Why This Repo Exists

Most of my strongest work is in private production repositories. Instead of publishing private code, I publish sanitized case studies that explain the systems, tradeoffs, and engineering decisions in a recruiter- and engineer-readable format.

If you are reviewing my profile, start with the case studies above and then visit my portfolio.

## Links

- Portfolio: https://mritunjai.dev
- GitHub: https://github.com/mritunjaichauhan
- LinkedIn: https://linkedin.com/in/mritunjai-chauhan-903607251
