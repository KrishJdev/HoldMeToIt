# HANDOFF.md

> **Canonical Handoff State** — Single persistent handoff file. Update in place at session end.  
> **Last updated:** 2026-09-03  

---

## Active Project & Stack

- **Project:** HoldMeToIt (Gamified Study Accountability & Challenge Management Platform)
- **Stack Status:** **LOCKED — Next.js 14+ Reference Architecture**
  - *Frontend & Fullstack:* Next.js 14+ (App Router), TypeScript 5.x, Tailwind CSS, shadcn/ui
  - *Database & Auth:* PostgreSQL (Supabase / Neon), Prisma ORM, Auth.js (Discord OAuth 2.0 Provider)
  - *Testing & Validation:* Vitest (domain math unit tests), Zod (boundary schema validation)
- **Database & Auth Requirement:** Relational PostgreSQL + Discord OAuth (non-negotiable core invariants)
- **Archive Policy:** Clean repo. No legacy codebase or quarantined archives present.

---

## Session Notes

- **2026-09-05 (Session 4 — Comprehensive AGENTS.md Production & Protocol Harmonization):**
  - Applied the `project-documentation` engineering skill to author the production-grade [AGENTS.md](file:///e:/Projects/HoldMeToIt/AGENTS.md).
  - Defined the 4-agent vertical roles: Data & Identity, Scoring & Engine, Participant UI, and Admin Operations & Broadcaster.
  - Formally locked Candidate A (Next.js 14+ App Router, Prisma, PostgreSQL, Auth.js, Tailwind, Vitest) as the authoritative reference stack.
  - Enumerated explicit technology rejections: banned NoSQL/MongoDB, custom password/email auth, Redux, GraphQL, in-browser web timers, and 24/7 bot daemons in P0.
  - Ratified Foundational Stack & Product Laws L1–L9, embedding the Cumulative Catch-Up Deficit Model, Second-Level Clock Precision (`HH:MM:SS`), Dual-Failure Accountability Invariant, and Pure Domain Isolation.
  - Specified the end-to-end automated quality matrix covering User Journeys J1–J6.
  - **NEXT STEP (exact):** Proceed with repository scaffolding for **Slice 1 (WU-1.1)**: Next.js 14 App Router, Tailwind CSS theme, and design system primitives.

---

## Sources of Truth

- **Product Features & Build Order:** `FEATURES.md`
- **Architecture Blueprint & Conventions:** `ARCHITECTURE.md`
- **Multi-Agent Protocol & Stack Laws:** `AGENTS.md`
- **Implementation Work Units:** `EXECUTION_PLAN.md`
- **Developer Setup & Run:** `README.md`
- **Sprint / Session Memory:** `HANDOFF.md` (this file)

---

## Development Strategy & Milestones (Vertical Slices)

| Slice | Focus | Status | Scope | Test Verification Targets |
| :--- | :--- | :---: | :--- | :--- |
| **Slice 1** | Foundation & Auth | ⬜ Queued | Next.js scaffold, Prisma models, Discord OAuth | `npm run build` green, OAuth mock session verified |
| **Slice 2** | Challenge Engine | ⬜ Queued | Creator wizard, team assignment, validation DTOs | Domain validation 6/6 green, team tests pass |
| **Slice 3** | CSV Ingestion & Logs | ⬜ Queued | Papaparse parser, batch transaction, override grid | 100-row batch commits in <1.5s, preview table |
| **Slice 4** | Leaderboard & Streaks | ⬜ Queued | Streak math, grace passes, podium UI, dashboard | Streak math 100% green, query <200ms |
| **Slice 5** | Accountability & Discord | ⬜ Queued | Punishment ledger, clearance modal, Webhook embed | Discord embed payload verified, clearance flow |
| **Slice 6** | E2E Release Verification | ⬜ Queued | Playwright automated user journeys J1–J6 | All 6 E2E user journeys green |

---

## Branching & Workflow

- **Active Development Branch:** `dev`
- **Stable Production Branch:** `main`
- **Feature Branches:** `feature/<slice_name>` (branched from `dev`, merged via PR to `dev`)
- **Rules:** Never force-push or clean uncommitted files; use Conventional Commits (`feat:`, `fix:`, `docs:`, `test:`, `refactor:`, `chore:`).
