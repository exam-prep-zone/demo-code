# OnlyMock — Claude Instruction Manual

## What This Project Is

Ed-tech PWA for Indian government exam aspirants (SSC, Banking, Railways, EPFO, UPSC single-day, State PCS, Defence).
Mobile-first. Single plan ₹49/month via Razorpay. No auto-renewal.

## Stack

- Framework: Next.js (App Router) — PWA, mobile-first
- Language: TypeScript — strict mode ON
- DB: PostgreSQL via Prisma ORM
- Payment: Razorpay
- Storage: S3/R2 (question images only — URL referenced in DB)
- Auth: Email + Password. Email verification mandatory. Single device session.

## Commands

```
npm run dev          # Start dev server
npm run build        # Production build
npm run lint         # ESLint check
npm run typecheck    # tsc --noEmit
npm run test         # Jest
npm run db:push      # Prisma DB push
npm run db:studio    # Prisma Studio
```

## Folder Structure

```
src/
├── app/             # Next.js App Router pages
│   ├── (public)/    # Home, Login, Signup, Pricing, Static pages
│   ├── (auth)/      # Progress, Practice, Mock, PYQ, Profile — requires login
│   └── admin/       # Admin panel — separate login — /admin
├── components/      # Shared UI components
├── lib/             # DB client, utils, helpers
├── hooks/           # Custom React hooks
├── types/           # Shared TypeScript types
└── emails/          # Email templates (5 templates)
```

## Two Website States

- **Before login:** Home Page is default. All nav → Login page. Logo stays on Home.
- **After login:** Progress Page is default. Home hidden. Nav shows user's name.

## Key Rules — Always Follow

- Never expose stack traces to client — use generic error messages
- Auth check on every (auth) route — redirect to login if not authenticated
- Single device session — new login invalidates previous session token
- Login block after 10 failed attempts — 30 min lockout
- Server-side mock timer — never trust client time for mock tests
- Practice marking: +3 / -1 / 0 (fixed, standardized)
- Mock marking: set by Admin per exam — read from DB, never hardcode
- Score calculation: latest 50 questions accuracy only
- Max 3 exams per user — enforce on selection
- Question images: always use cloud URL from DB, never local paths
- Pack expiry: show 5-day banner on ALL pages when pack expiring soon
- PWA install prompt: once per day only

## Language System

- English always available (fixed)
- 1 regional language per user (chosen in Profile) — up to 15 supported
- Separate file per language per subject stored in DB
- Max 2 options in test dropdown (English + user's regional language)
- English subjects always in English even in regional mode

## Free vs Paid

- Free: limited access — show upgrade prompt on locked features
- Paid: full access — ₹49/month — no auto-renewal — Razorpay

## Off-limits — Never Touch

- Never read: .env, .env.\*, node_modules/, .next/, prisma/migrations/
- Never run: rm -rf, curl without explicit approval
- Never modify: DB schema without showing migration plan first
- Never hardcode: API keys, secrets, pricing, exam patterns

## Context Management

- Use /compact when context feels heavy
- Use /clear between unrelated features
- Write handoff notes before ending long sessions
