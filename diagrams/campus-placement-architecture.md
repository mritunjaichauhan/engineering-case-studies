# Campus Placement Architecture

```text
Users
  |
  +-- Students
  +-- Placement teams
  +-- Recruiters / company contacts
  +-- Interviewers
  +-- Platform operators
  |
  v
Web app / mobile app / admin surfaces
  |
  v
Auth, org context, RBAC, tenant selection
  |
  +-----------------------------+
  |                             |
  v                             v
Convex realtime backend         Cloudflare Workers API
  |                             |
  |                             +-- Hono
  |                             +-- oRPC
  |                             +-- OpenAPI contracts
  |                             +-- API rate limits
  |                             +-- HMAC-signed model proxying
  |
  +-- organizations
  +-- users
  +-- students
  +-- companies
  +-- jobs
  +-- rounds
  +-- applications
  +-- interviews
  +-- reports
  +-- credits
  +-- audit logs
  +-- notifications
  +-- placement stats
```

## Design Notes

- Tenant boundaries must be enforced in schema access, UI state, and API handlers.
- Administrative actions should emit audit records.
- Expensive AI and assessment actions need rate limits and credit accounting.
- High-read counters should avoid repeatedly scanning large collections.
