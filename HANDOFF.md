# HANDOFF.md

> **Canonical Handoff State** — Single persistent handoff file. Update in place at session end.  
> **Last updated:** 2026-09-03  

---

## Active Project & Stack

- **Project:** HoldMeToIt (Gamified Study Accountability & Challenge Management Platform)
- **Stack Status:** **UNLOCKED — Pending Group Consensus**
  - *Candidate A (Default Reference):* Next.js 14+ (App Router), TypeScript, Tailwind CSS, Supabase (PostgreSQL), Prisma ORM
  - *Candidate B (Decoupled PERN):* React (Vite), Node.js (Express), PostgreSQL, Prisma
  - *Candidate C (Decoupled Python):* React (Vite), FastAPI (Python), PostgreSQL, SQLAlchemy
- **Database & Auth Requirement:** Relational PostgreSQL + Discord OAuth (non-negotiable core invariants)
- **Archive Policy:** Clean repo. No legacy codebase or quarantined archives present.

---

## Session Notes

- **2026-09-03 (Session 3 — Real Spreadsheet Alignment, Extreme Simplification & Git Deployment):**
  - Scrubbed all entrance exam references (JEE/NEET/UPSC) across docs and wireframe to focus purely on general Discord community study battles.
  - Analyzed the community's exported Google Spreadsheet (`BEES` vs `BUTTERFLIES` team battle, individual declared study targets, Tuesday-to-Monday daily YPT logs, mandatory weekly to-do goals, and community Punishment PFP).
  - Radically simplified the user interface for extreme clarity: Big match scoreboard, dedicated "Log Your Study Hours" card (Select Day $\rightarrow$ Enter Hours $\rightarrow$ Add), interactive Weekly Goals checklist, clean 6-column Community Standings table, and discreet Mod / Host controls.
  - Generated full-page high-resolution PNG mockups (`wireframe/preview_member_full.png`, `wireframe/preview_mod_full.png`) for instant Figma drag-and-drop.
  - Placed root `index.html` and synchronized branches `prototyping`, `prototype`, and `gh-pages` with remote `origin` on GitHub.
  - Un-ignored and committed core documentation specifications (`AGENTS.md`, `ARCHITECTURE.md`, `EXECUTION_PLAN.md`, `FEATURES.md`, `HANDOFF.md`) and `.agents/` operational skills to git for seamless cross-device synchronization.
  - **NEXT STEP (exact):** Await team review of the prototype on Figma or GitHub Pages. Once candidate tech stack consensus is locked, proceed to **Phase 2 / Slice 1 (WU-1.1)** repository scaffolding.

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
