# Delivery Decisions and Lessons

Record durable product, technical, and delivery-process decisions.

## Decision log
| Date | Decision | Reason | Consequences / follow-up |
|---|---|---|---|
| 2026-11-12 | **Provisional architecture recommendation:** Next.js with TypeScript for the caregiver web UI, deployed on Vercel; Supabase for Postgres, Auth, and server-side Edge Functions. Use Edge Functions for backend orchestration and calls to external AI services, keeping provider secrets server-side. | The repository has no application code or existing stack to preserve. This matches the user's preference for Vercel UI and Supabase data, auth, and computation. Supabase documents Edge Functions for TypeScript server-side integrations and anonymous Auth; Vercel documents native Next.js deployment. | This is a recommended baseline, not an implemented or production-validated architecture. Confirm service plans, Canadian data-handling requirements, and deployment setup before implementation. Prefer a Supabase Canada Central project if available and suitable, but region choice is not yet confirmed. |
| 2026-11-12 | **Provisional identity and persistence recommendation:** Do not require caregiver sign-up for story creation. Use Supabase anonymous Auth to associate a minimal daily successful-generation counter with a browser-level anonymous user; do not persist story text, situation descriptions, character names, or child profiles in the MVP database. | The product definition says accounts are not required unless needed, and the daily limit must be consistent across refreshes and sessions. Anonymous Auth supports an authenticated experience without collecting email or password. Minimizing retained story inputs supports the privacy requirements. | Anonymous identity is not a verified person-level limit: clearing browser data or using another device can create another identity. Confirm whether this is acceptable for cost control or whether caregiver accounts/stronger abuse controls are needed. Define counter retention and cleanup before implementation. |
| 2026-11-12 | **AI-provider selection deferred:** Invoke text and image generation through server-side functions, but do not select a vendor yet. | No provider, budget, model quality, service terms, or Canadian data-processing requirements are established in the repository. Choosing a vendor now would be an unsupported assumption. | Compare providers before AI integration, including text and illustration capability, child-safety controls, cost, data use/retention, and service availability in the chosen region. The AI provider is an open architecture decision, not a confirmed selection. |
| 2026-11-12 | **Configuration and deployment recommendation:** Keep AI credentials and privileged Supabase credentials in server-side secret stores; expose only client-safe configuration to the browser. Use separate local, preview, and production configuration and verify environment separation before launch. | Supabase Edge Functions support server-side secrets, and Vercel supports Git-based deployments and preview environments. The repository currently has no deployment or configuration files. | Do not commit credentials. Exact environment variable names, project separation, plans, and deployment settings remain to be established in the development-environment issue. |

### Options reviewed

| Option | Benefits | Trade-offs | Assessment |
|---|---|---|---|
| Next.js UI and backend on Vercel, with Supabase for database/Auth | Fewer service boundaries for application requests; Vercel's native Next.js workflow. | Places business logic and AI orchestration on Vercel rather than the user's preferred Supabase computation; still needs secure database access. | Feasible fallback if Supabase Edge Functions prove unsuitable. |
| Next.js UI on Vercel; Supabase Postgres, Auth, and Edge Functions | Matches the user's stated service preference; managed database/auth and server-side TypeScript functions are available. | Adds a service boundary, function-to-database/provider configuration, and cross-origin/authentication considerations. | Recommended provisional baseline; validate with a small technical spike before committing to production. |
| Build without user identity or persistent usage records | Simplest data model and least retained data. | Cannot reliably apply the required daily limit across refreshes or sessions. | Does not meet the stated generation-limit acceptance criteria without a separate identity/counter mechanism. |

### Open questions and assumptions

- Which text and image-generation providers meet the product's safety, quality, cost, and data-processing needs?
- Is a browser-level anonymous identity sufficient for the two-successful-stories-per-day limit, or is a caregiver account or stronger abuse control required?
- Is Canada Central the required Supabase data region? A region choice controls primary database location but does not, by itself, establish legal or privacy compliance.
- What retention period and deletion mechanism should apply to anonymous identities and daily usage counters?
- Which Vercel and Supabase plans, environments, and operational limits fit the expected budget?
- This recommendation assumes an adult-operated responsive web app, no child account, no saved-story/profile feature, and no need to retain full story inputs after a response is delivered. These assumptions follow the MVP scope but must be checked against final provider behavior and privacy disclosures.

### Evidence reviewed

- Repository inventory (`git ls-files`) and README: only project/delivery documentation is present; no app source, dependency manifests, tests, or deployment configuration exist.
- Issue [#1 — Confirm architecture and key technical decisions](https://github.com/parniyanroosta/ai-powered-story-generator/issues/1), including its goal and acceptance criteria.
- [US-26: Enforce the daily generation limit](../docs/USER_STORIES_ACCEPTANCE_CRITERIA.md) and [US-28: Protect caregiver and child information](../docs/USER_STORIES_ACCEPTANCE_CRITERIA.md).
- [Supabase Edge Functions](https://supabase.com/docs/guides/functions), [Supabase Auth](https://supabase.com/docs/guides/auth), [anonymous sign-ins](https://supabase.com/docs/guides/auth/auth-anonymous), [available regions and data residency](https://supabase.com/docs/guides/platform/regions), and [Row Level Security](https://supabase.com/docs/guides/database/postgres/row-level-security).
- [Vercel's Next.js deployment documentation](https://vercel.com/docs/frameworks/full-stack/nextjs).

## Delivery lessons
Record recurring friction, incorrect assumptions, and evidence-based improvements. Prefer specific, actionable lessons over general observations.
