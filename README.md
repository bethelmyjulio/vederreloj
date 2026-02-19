# Seasonal Skill Builder

Seasonal Skill Builder is a product spec and implementation blueprint for an off-season hunter training application focused on retention, structured progression, and measurable skill gains.

## Repository purpose

This repository currently contains:

- A polished master build prompt for AI coding tools.
- A technical MVP architecture plan that can be used to scaffold the first production-ready version.

## Documents

- `docs/master-build-prompt.md` — direct build prompt suitable for Antigravity/Codex-style tools.
- `docs/mvp-architecture.md` — implementation-ready architecture, data model, API shape, and phased rollout plan.

## MVP priorities

1. Authentication
2. Dashboard
3. Module system
4. Shooting and fitness logging
5. Basic gamification

## Suggested stack

- Frontend: React (Next.js App Router)
- Backend: Next.js Route Handlers (or Express/Fastify if separated)
- Auth: Email/password + optional Google OAuth
- DB: PostgreSQL + Prisma
- Charts: Recharts
- Hosting: Vercel/Render + managed Postgres
