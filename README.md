# HoldMeToIt ⚡

> **Gamified Study Accountability & Challenge Management Platform**  
> Replacing manual Discord spreadsheets, YPT screenshot tracking, and host burnout with an automated challenge engine.

---

## 🎯 Overview & Mission

Study challenges in Discord communities (running weekly team accountability duels, productivity sprints, and study seasons) suffer from severe **Admin Burnout**. Community moderators spend 5–10 hours every week manually building complex spreadsheets, copy-pasting YPT daily timestamps across 20+ columns, calculating team hour differences, verifying individual to-do goals, and enforcing server Punishment PFPs.

**HoldMeToIt** automates the entire lifecycle of Discord study battles:
- **Instant Challenge Setup:** Hosts configure battle cycles (e.g. Tuesday–Monday), team rosters, and punishment rules in minutes.
- **Declared Individual Targets & Weekly Goals:** Each participant declares their own weekly study-hour target (e.g. 20h, 35h, 50h, 70h) and weekly to-do list goals.
- **Bulk CSV Ingestion:** Ingest study logs exported from Yeolpumta (YPT) in seconds, auto-populating daily hours (HH:MM:SS) and calculating decimal totals.
- **Team vs Team Battle Standings:** Real-time team totals (e.g. Bees vs Butterflies), current leader, hour difference, and completion percentages.
- **Server Accountability & Punishment PFP:** Automated tracking of weekly goal and target completion with an accountability workflow for the community's Punishment PFP.
- **Discord Integration:** Frictionless Discord OAuth login and one-click Webhook standings broadcasts to `#study-announcements`.

---

## 🛠️ Proposed Tech Stack Candidates (Pending Group Consensus)

> **Decision Status:** Open for group review and vote. The team will ratify one of the following candidate stacks based on members' collective background before scaffolding code:

### Candidate Comparison

| Dimension | Candidate A: Fullstack Next.js (Default Reference) | Candidate B: Decoupled PERN (React + Express) | Candidate C: Decoupled React + FastAPI (Python) |
| :--- | :--- | :--- | :--- |
| **Frontend** | Next.js 14+ (App Router) + Tailwind CSS | React (Vite) + Tailwind CSS | React (Vite) + Tailwind CSS |
| **Backend / API** | Next.js Server Actions & Route Handlers | Node.js (Express) REST API | Python (FastAPI) REST API |
| **Database & Auth** | Supabase (PostgreSQL + Discord OAuth) | PostgreSQL + Passport / Supabase | PostgreSQL + Supabase / Authlib |
| **ORM / Querying** | Prisma ORM | Prisma ORM / Drizzle | SQLAlchemy / SQLModel |
| **Best Fit For** | Speed of delivery, single repo, zero CORS, free Vercel hosting. | Clear division between Frontend & Backend teammates. | Teams with strong Python backgrounds for CSV data processing. |

---


## 📚 Multi-Agent Documentation Suite (Sources of Truth)

This project strictly adheres to the **Five Pillars of Multi-Agent Documentation**:

| Document | Primary Authority & Purpose |
| :--- | :--- |
| **[FEATURES.md](FEATURES.md)** | Absolute source of truth for **product behavior, screen layouts, UX intent, and phase tags** (`[P0]` to `[V2]`). |
| **[AGENTS.md](AGENTS.md)** | Absolute source of truth for **agent protocols, stack laws, git safety rules, and E2E quality matrix**. |
| **[ARCHITECTURE.md](ARCHITECTURE.md)** | Absolute source of truth for **Feature-First Clean Architecture, layer contracts, and database schema**. |
| **[EXECUTION_PLAN.md](EXECUTION_PLAN.md)** | Absolute source of truth for **work unit breakdown, Mermaid DAG, and verification gates**. |
| **[HANDOFF.md](HANDOFF.md)** | Single persistent file for **session memory, milestone status, and the immediate next step**. |

---

## 👥 Recommended Group Project Role Division

To prevent team members from colliding or encountering merge conflicts:

1. **Member 1 (Data & Ingestion Lead):**
   - Focus: `core/db/`, `prisma/schema.prisma`, `features/study-logs/data/`.
   - Deliverables: Database schema, CSV parser service, batch ingestion transactions.
2. **Member 2 (Challenge & Calculation Engine):**
   - Focus: `features/challenges/domain/`, `features/leaderboard/domain/`, `features/accountability/`.
   - Deliverables: Scoring math, streak rules, grace pass logic, Discord Webhook embed generator.
3. **Member 3 (Participant Experience UI):**
   - Focus: `app/(dashboard)/`, `features/leaderboard/presentation/`.
   - Deliverables: Personal cockpit dashboard, podium rankings, 7-day hours chart, streak badges.
4. **Member 4 (Admin Operations UI):**
   - Focus: `app/(admin)/`, `features/challenges/presentation/`, `features/study-logs/presentation/`.
   - Deliverables: Challenge creation wizard, CSV dropzone preview modal, manual override roster grid.

---

## 🚀 Getting Started (Once Scaffolded)

### 1. Prerequisites
- Node.js 18.17+ or 20.x
- A free [Supabase](https://supabase.com/) account
- A [Discord Developer Portal](https://discord.com/developers/applications) application for OAuth

### 2. Environment Setup
```bash
# Clone the repository
git clone https://github.com/your-org/hold-me-to-it.git
cd hold-me-to-it

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env.local
```

### 3. Local Development
```bash
# Run database migrations
npx prisma db push

# Start Next.js development server
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.
