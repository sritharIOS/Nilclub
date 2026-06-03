# NIL Club — Athlete Earnings Tracker

## What We're Building
A mobile app where student-athletes can view their NIL (Name, Image, Likeness) 
earnings from brand deals. Athletes see their total earnings, active deals, 
and payment history.

## Monorepo Structure
- apps/api — Next.js 16 App Router + Hono + Zod (API routes)
- apps/mobile — React Native 0.81 + Expo SDK 54 + Expo Router v4 (mobile app)
- packages/database — Drizzle ORM schema + queries + seed script (Neon Postgres)

## Tech Stack
- Monorepo: Turborepo + pnpm workspaces
- Mobile: React Native + Expo SDK 54, Expo Router v4
- API: Next.js 16 App Router, Hono, Zod validation
- Database: Drizzle ORM + Neon Postgres (@neondatabase/serverless)
- State: TanStack Query v5
- Language: TypeScript 5.x strict mode

## Domain Model
- Athlete: has name, sport, school
- Deal: belongs to athlete, has brand name, value (stored in cents), status
- Payment: belongs to deal, has amount (stored in cents), status, paid_at date

## Deal Statuses
- pending, active, completed, cancelled

## Payment Statuses
- paid, pending, failed

## Key Conventions
- TypeScript strict mode, no `any`
- Money stored as integer cents (e.g. $15,000 = 1500000)
- Always validate API inputs/outputs with Zod
- No authentication — hardcode athleteId = 1 (Marcus Johnson)
- Small focused files, proper error handling

## API Endpoints
- GET /api/athletes — list all athletes
- GET /api/athletes/:id — get athlete profile
- GET /api/athletes/:id/deals — get athlete's deals
- GET /api/athletes/:id/earnings — get earnings summary (paid vs pending)
- GET /api/deals/:id/payments — get payment history for a deal

## Mobile Screens
1. Earnings Overview — matches mockup exactly (athlete header, earnings card, deals list)
2. Deal Detail — payment history for a tapped deal

## Both Screens Must Have
- Loading state
- Error state with retry
- Pull-to-refresh

## Seed Data (must match mockup exactly)
Marcus Johnson — Basketball, Duke University
- Nike deal: $15,000 total
  - Payment 1: $5,000 paid
  - Payment 2: $5,000 paid
  - Payment 3: $4,500 pending (note: intentionally $500 short of deal value)
- Gatorade deal: $8,000, pending, 0 of 2 payments
- EA Sports deal: $6,500, completed, 4 of 4 payments

Add 2+ more athletes with varied statuses.

## Commands
- pnpm dev — start all apps
- pnpm db:push — push schema to Neon
- pnpm db:seed — seed sample data
- pnpm build — build all apps

## What NOT to Build
- No auth/login
- No automated tests (mention in README)
- No deployment
- No dark mode
- No animations
