# Campus Placement Management System

## Summary

A multi-tenant campus placement and student management platform for placement teams, students, recruiters, interviewers, and platform operators.

The system covers placement drives, student profiles, company workflows, job applications, interview scheduling, assessments, AI interviews, coding practice, credit accounting, audit logs, notifications, compliance reporting, and admin control surfaces.

## My Role

Full-stack product engineering at Hirecentive, working across web app flows, backend data modeling, role-based access control, realtime product data, API boundaries, and assessment-related infrastructure.

## Problem

University placement teams need more than a job board. They need a system that can coordinate students, recruiters, internal staff, interviewers, drives, rounds, applications, offers, reporting, and compliance while keeping tenant data isolated.

The hard part is not just the UI. The hard parts are:

- Multi-tenant access boundaries
- Role-specific workflows
- Realtime updates across placement activity
- Searchable and indexable student/job/application data
- Auditability for administrative actions
- Reliable credit usage and assessment attempt tracking
- Safe AI and coding-assessment infrastructure

## Product Scope

- Organization and role management
- Student profiles, resumes, academic details, eligibility, and placement status
- Company and recruiter relationship management
- Placement drives, jobs, rounds, applications, and results
- Interview scheduling and reports
- Practice tests and coding-assessment primitives
- Credit allocation, ledger entries, and platform-level allocation batches
- Notifications, email logs, preferences, and reminders
- Audit logs and compliance reporting
- Web app, API layer, control-plane/admin flows, and mobile surfaces

## Engineering Highlights

- Modeled a large Convex domain with 30+ product tables and 100+ query indexes.
- Used tenant-aware data access patterns to separate organizations and role-specific workflows.
- Integrated WorkOS-style organization, membership, role, and permission concepts.
- Used sharded counters for high-read application-count style data.
- Added rate limiting at multiple boundaries for user sync, invites, interviews, resume extraction, Gemini usage, Judge0, and API access.
- Used HMAC-signed proxying patterns for model-related realtime/API traffic instead of exposing sensitive credentials to clients.
- Kept frontend, backend, API, and mobile surfaces aligned through shared packages and contract-first APIs.
- Included Playwright coverage for important user flows.

## Architecture

```text
Web App / Admin Surfaces / Mobile App
        |
        v
Shared packages, auth context, role checks, schemas
        |
        +--------------------+
        |                    |
        v                    v
Convex Realtime Backend   Cloudflare Workers API
        |                    |
        v                    v
Tenant data, audits,      Hono + oRPC + OpenAPI,
credits, jobs, apps,      rate limits, model/API proxying
interviews, reports
```

## Key Tradeoffs

- Convex was useful for realtime operational product data, but the schema needed careful indexing and tenant-aware access patterns.
- Placement teams need flexible workflows, but too much flexibility can make reporting and permissions fragile. The model keeps core concepts explicit: jobs, rounds, applications, results, interviews, credits, and audits.
- AI and coding features need separate rate limits and attempt accounting because they are costly and abuse-prone compared with normal dashboard reads.

## Tech Stack

- Next.js
- React
- TypeScript
- Convex
- Cloudflare Workers
- Hono
- oRPC
- OpenAPI
- WorkOS-style RBAC
- Expo
- Tailwind CSS
- Playwright

## What I Learned

- Placement software is closer to operational infrastructure than a simple student portal.
- Multi-tenant systems need clear boundaries in schema, API, UI, and admin workflows.
- Audit logs, rate limits, and credit ledgers are not optional once AI and assessments enter the product.
- Recruiter-facing SaaS needs both polished UI and boringly reliable backend accounting.
