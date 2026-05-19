# RebuildCV AI Resume SaaS

## Summary

An AI resume and career SaaS product for resume analysis, ATS scoring, job-description optimization, resume versions, PDF exports, CareerGPT guidance, subscriptions, credits, invoices, influencer campaigns, and university cohorts.

## My Role

Full-stack SaaS and monetization engineering across AI workflows, billing, invoices, database schema, user journeys, and admin workflows.

## Problem

Resume builders often stop at editing and templates. A useful career SaaS needs the complete loop:

- Understand a user's resume
- Compare it against target jobs
- Suggest improvements
- Save versions
- Export clean PDFs
- Provide career guidance
- Gate usage with credits/subscriptions
- Support invoices, promotions, affiliates, cohorts, and admin operations

## Product Scope

- Resume analysis and ATS-oriented feedback
- Job-description matching and optimization
- Resume versioning
- Template PDF exports
- CareerGPT chat with resume and career context
- Razorpay subscriptions and credit purchases
- Zoho Books invoice integration
- Influencer promo ledger and attribution
- University/cohort management
- Admin dashboards and transaction tracking

## Engineering Highlights

- Built CareerGPT around six modes: career plan, resume review, interview prep, job search, skill gap, and salary offer.
- Routed Google model usage through Cloudflare AI Gateway using the Vercel AI SDK and `@ai-sdk/google`.
- Used AI Gateway cache headers with a 3600-second TTL for supported requests.
- Modeled D1/SQLite tables for users, credits, universities, influencer promos, promo usage, subscriptions, resumes, resume versions, payments, suggestions, conversations, and messages.
- Supported multiple monetization paths: subscriptions, credit packs, promo codes, influencers, university cohorts, and invoices.
- Integrated payment and invoice lifecycle with Razorpay and Zoho Books.

## Architecture

```text
Next.js App
   |
   +--> Resume and Career UX
   |        |
   |        v
   |     Resume versions, ATS/JD workflows, PDF exports
   |
   +--> CareerGPT
   |        |
   |        v
   |     Vercel AI SDK + @ai-sdk/google
   |        |
   |        v
   |     Cloudflare AI Gateway
   |
   +--> Billing/Admin
            |
            v
         Razorpay + Zoho Books + D1/SQLite
```

## Key Tradeoffs

- AI chat becomes much more useful when it has structured resume and career context, but that requires careful persistence of conversations, messages, summaries, and selected resume context.
- Payments and invoices need to be treated as product infrastructure, not just checkout UI.
- Influencer and cohort acquisition require attribution tables and admin workflows early, otherwise campaign performance becomes hard to reason about later.

## Tech Stack

- Next.js
- TypeScript
- Cloudflare Workers
- OpenNext
- D1
- KV
- Cloudflare AI Gateway
- Vercel AI SDK
- `@ai-sdk/google`
- Razorpay
- Zoho Books
- Drizzle ORM
- Tailwind CSS

## What I Learned

- A credible AI SaaS needs monetization, lifecycle emails/invoices, admin tools, and support workflows, not only prompts.
- Career and resume products need version history because users iterate toward specific jobs.
- Billing, promo attribution, and invoice sync should be designed as durable workflows from the beginning.
