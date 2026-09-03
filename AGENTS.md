# AGENTS.md — Multi-Agent Coordination Protocol & Engineering Standards

> **Project:** HoldMeToIt (Gamified Study Accountability & Challenge Management Platform)  
> **Repository:** Absolute source of truth. All contributing human engineers and AI agents are equal peers.  
> **Rule:** No single agent owns the codebase. Quality gates and stack laws apply unconditionally.  
> **Last updated:** 2026-09-03  

---

## 1. Agents & Responsibilities

| Role / Agent ID | Scope / Focus | Primary Layer Responsibilities |
| :--- | :--- | :--- |
| **Data & Ingestion Agent** | Database schema, CSV parsing engine, atomic ingestion transactions | Prisma schemas, Supabase migrations, CSV parser service, validation DTOs |
| **Scoring & Engine Agent** | Leaderboard calculations, streaks, grace days, punishment triggers | Domain math services, aggregation queries, Discord webhook payloads |
| **Participant UI Agent** | Student-facing views, responsive dashboards, streak gauges | Next.js Server & Client components, Tailwind UI, chart visualizations |
| **Admin Operations Agent** | Host wizards, CSV dropzone, manual adjustment grids, clearance modals | Admin consoles, data grids, modal dialogs, form mutations |

### 1.1 Equality & Collaboration Posture
- All agents and human contributors possess equal authority.
- No agent shall unilaterally overwrite another agent's work without running pre-checks and verifying behavioral regression.
- Work is broken down into parallel-safe vertical slices to minimize file collisions.

---

## 2. Development Strategy (Vertical Slices)

We adhere strictly to **Feature-First Vertical Slices**. Work units are sliced through all necessary layers for a specific capability rather than horizontally across all files.

### 2.1 Anatomy of a Feature Slice
```text
features/<feature_name>/
├── domain/            # Pure business entities, calculation math, zero framework imports
├── data/              # Prisma models, repository implementations, CSV parsers, queries
├── presentation/      # UI components, state hooks, responsive views
└── api/               # Next.js Route Handlers / Server Actions
```

### 2.2 Definition of Done (DoD) per Slice
A vertical slice is only complete when:
1. **Typesafe:** Zero TypeScript compiler errors (`tsc --noEmit` passes).
2. **Tested:** Unit tests for domain logic and math pass with 100% green exit.
3. **Designed States Handled:** Loading skeleton, Empty state, and Error fallback screens are fully implemented (Product Law L6).
4. **Mobile Verified:** Layout renders cleanly without overflow on a 360px viewport.
5. **Documented:** Session changes recorded in `HANDOFF.md`.

---

## 3. Baseline Pre-Checks (Before Every Task)

Every agent or developer beginning a task must follow this exact sequential checklist:
1. Read `AGENTS.md` (this file) to re-align on stack laws and git safety rules.
2. Read `HANDOFF.md` to identify the active milestone and the exact **NEXT STEP**.
3. Read `FEATURES.md` to review the authoritative UX and product intent for the targeted feature.
4. Run `git status` and `git log -n 3` to verify workspace cleanliness.
5. Inspect the specific feature directory before writing code; never assume what exists.
6. **No Redundant Implementation Plans:** If the task is already scoped in `EXECUTION_PLAN.md`, do not generate a duplicate design document. Proceed immediately to execution.

---

## 4. Git Workflow & Safety Rules

### 4.1 Branching Strategy
| Branch | Purpose | Merge Criteria |
| :--- | :--- | :--- |
| `main` | Production-ready, deployable release code | Peer review + all E2E journeys green |
| `dev` | Shared integration branch for active sprint | All unit/integration tests passing |
| `feature/<name>` | Vertical slice development branch | Slice DoD satisfied |
| `fix/<name>` | Hotfixes and defect resolutions | Targeted regression test passing |

### 4.2 Conventional Commits
All commits must follow the conventional commit format:
- `feat(scope): ...` (New capability or feature)
- `fix(scope): ...` (Defect resolution)
- `docs(scope): ...` (Documentation changes)
- `refactor(scope): ...` (Code changes without behavior changes)
- `test(scope): ...` (Adding or updating tests)
- `chore(scope): ...` (Dependency updates, tooling configs)

### 4.3 Strictly Forbidden Git Commands
The following commands are **strictly prohibited** in all environments:
- `git reset --hard` (Data loss hazard)
- `git clean -fd` (Unrecoverable file deletion)
- `git push --force` or `git push -f` (Overwriting shared history)
- Rebasing shared public branches (`dev` or `main`)

---

## 5. Conflict Resolution Protocol

When encountering conflicting code or architectural divergence:
1. **STOP:** Halt automated code generation immediately.
2. **INSPECT:** Read git blame and recent commit logs to understand the original author's intent.
3. **UNDERSTAND:** Evaluate which approach adheres more strictly to `FEATURES.md` and the Stack Laws.
4. **EVALUATE:** If the existing code functions and satisfies tests, preserve it. Improve incrementally rather than replacing wholesale.
5. **DECIDE & LOG:** Document any forced deviations in `HANDOFF.md` under session notes.

---

## 6. Technology Stack (Pending Group Consensus)

> **Status:** **UNLOCKED / PENDING GROUP RATIFICATION**  
> The team will review candidate architectures and vote on the final stack based on member familiarity and project velocity. Once the group reaches consensus, this section will be locked.

### 6.1 Candidate Stack Architectures Under Evaluation

| Dimension | Candidate A: Fullstack Next.js (Default Reference) | Candidate B: Decoupled PERN (React + Express) | Candidate C: Decoupled React + Python (FastAPI) |
| :--- | :--- | :--- | :--- |
| **Frontend** | Next.js 14+ (App Router) + Tailwind CSS | React (Vite) + Tailwind CSS | React (Vite) + Tailwind CSS |
| **Backend / API** | Next.js Server Actions & Route Handlers | Node.js (Express.js) REST API | Python (FastAPI) REST API |
| **Database & Auth** | Supabase (PostgreSQL + Discord OAuth) | PostgreSQL + Passport.js / Supabase Auth | PostgreSQL + Supabase / Authlib |
| **ORM / Querying** | Prisma ORM | Prisma ORM / Drizzle | SQLAlchemy / SQLModel |
| **Pros** | Single repo, zero CORS, built-in Discord auth, free Vercel hosting. | Traditional separation of frontend/backend developers; easy mental model. | Great if team has Python members comfortable with pandas for CSV data. |
| **Cons** | Next.js App Router learning curve for React beginners. | Requires managing two separate servers, CORS, and auth middleware. | Managing two repos and Python virtualenvs across team machines. |

### 6.2 Architectural Non-Negotiables (Regardless of Stack Selected)
Whatever candidate the team ratifies, the following architectural principles remain mandatory:
- **Relational Integrity:** The database must be relational (PostgreSQL preferred). No document stores (like MongoDB) for relational challenge/team standings logic.
- **Discord OAuth Primacy (Law L4):** Avoid custom password/email registration for MVP. Leverage Discord OAuth so users authenticate seamlessly.
- **Type Safety & Validation:** Input payloads (especially CSV ingestion and score overrides) must be strictly validated at the API boundary (e.g. Zod in TypeScript, Pydantic in Python).
- **Lean P0 Notifications:** Use Discord Webhooks (HTTP POST) for standings broadcasts in Phase 1 rather than hosting a 24/7 bot daemon.

---

## 7. E2E Quality Matrix & User Journeys (J1–J6)

Every release candidate must pass these concrete user journeys:

```mermaid
journey
    title HoldMeToIt E2E Quality Matrix
    section J1: Auth
      Login via Discord: 5: Participant
      Profile Created in DB: 5: System
    section J2: Setup
      Admin Creates Challenge: 5: Admin
      Assigns Teams (N=1,2,Squad): 5: Admin
    section J3: Ingestion
      Admin Uploads YPT CSV: 5: Admin
      Leaderboard Updates Instantly: 5: System
    section J4: Corrections
      Admin Edits Hours Inline: 4: Admin
      Delta Reflected in Streak: 5: System
    section J5: Accountability
      Missed Target Triggers Grace Pass: 5: System
      Depleted Passes Flag Punishment: 5: System
    section J6: Broadcast
      Admin Clicks Discord Webhook: 5: Admin
      Rich Embed Appears in Channel: 5: Discord
```

### J1: Discord OAuth Login & Profile Provisioning
- **Trigger:** Guest navigates to `/` and clicks "Login with Discord".
- **Action:** Authenticates with Discord OAuth; redirected to `/dashboard`.
- **Database Assertion:** Record exists in `User` with matching `discordId`, `username`, and `avatarUrl`.
- **Laws Gated:** L4 (Discord Identity Primacy).

### J2: Admin Challenge Creation & Team Rostering
- **Trigger:** Authenticated Admin opens `/admin/challenges/new`.
- **Action:** Submits 2-week challenge with target of 28 hrs/week, 1 grace day, Duo mode ($N=2$).
- **Database Assertion:** `Challenge` record created with status `UPCOMING`, team size $2$, target hours $28$.
- **Laws Gated:** L1 (Single Entity Unity), L2 (Spreadsheet Exorcism).

### J3: CSV Bulk Ingestion & Immediate Leaderboard Propagation
- **Trigger:** Admin uploads a 100-row YPT export `.csv` via `/admin/challenges/:id/import`.
- **Action:** Reviews mapped columns and clicks "Commit Ingestion".
- **Database Assertion:** `StudyLog` table populated with 100 entries; leaderboard query reflects new ranking in $<400\text{ms}$.
- **Laws Gated:** L2 (Spreadsheet Exorcism), L6 (Zero-State & Error Handling).

### J4: Manual Hours Override & Audit Logging
- **Trigger:** Host clicks an hours cell in `/admin/challenges/:id/roster` to resolve a participant's timer crash.
- **Action:** Edits value from `0.0` to `4.5` hours; hits enter.
- **Database Assertion:** `StudyLog` updated or inserted with `source = 'ADMIN_OVERRIDE'`; streak recalculates.
- **Laws Gated:** L5 (Admin Override Absolute).

### J5: Grace Pass & Punishment Trigger Assertion
- **Trigger:** End of calculation cycle reached.
- **Action:** Engine evaluates members whose study hours fell below target.
- **Assertion:** 
  - If member has remaining grace passes $\rightarrow$ `gracePasses` decremented by 1, status remains `ON_TRACK`.
  - If grace passes exhausted $\rightarrow$ record inserted in `PunishmentLedger` with status `FLAGGED`.
- **Laws Gated:** L3 (Forgiving Gamification).

### J6: Discord Webhook Broadcast Trigger
- **Trigger:** Admin clicks "Broadcast Standings" on active challenge page.
- **Action:** Server formats JSON embed payload and POSTs to Discord Webhook URL.
- **Assertion:** HTTP 204 received from Discord; podium and punishment watchlist visible in target channel.
- **Laws Gated:** L2 (Spreadsheet Exorcism).
