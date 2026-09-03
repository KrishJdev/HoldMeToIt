# HoldMeToIt — Comprehensive Feature Specification

> **Purpose:** The complete product feature specification — every feature, screen, and workflow across the full product vision (MVP → V2).  
> **Source of Truth:** Repository root. Absolute override authority on product behavior, screen layouts, and roadmap phases.  
> **Rule:** Replicate behavior and UX intent, not legacy spreadsheets.  
> **Last updated:** 2026-09-03  

---

## 1. Product Overview & Quality Bar

### 1.1 Mission & Unique Value Proposition
**HoldMeToIt** is a gamified study accountability and challenge management platform engineered to eradicate "Admin Burnout" and fragmented tracking across Discord study communities.

It replaces the chaotic loop of manual Google Sheets calculations, Yeolpumta (YPT) screenshot reviews, and unstructured Discord message dumps with a single, automated, web-native challenge engine. Organizers configure challenges in minutes, ingest study data via CSV or manual logs, and let the system calculate standings, streaks, winners, and punishment statuses automatically.

### 1.2 Target Persona & Community Constraints
- **Primary Persona (The Host / Admin):** Community moderators running weekly competitive study battles for 10–100+ server members. Currently spending 5–10 hours/week manually copy-pasting YPT daily times into spreadsheets, calculating differences, and enforcing server accountability punishments.
- **Secondary Persona (The Grinder / Participant):** Discord community members taking part in weekly team study duels and accountability sprints. Each participant declares their own weekly study-hour target and weekly to-do list goals before the battle. They track hours via YPT/stopwatches, cheer on their team, and must meet their declared goals to avoid the community's Punishment PFP.
- **Ecosystem Constraints:**
  - Users already coordinate on **Discord**; any non-Discord identity mechanism introduces friction.
  - Primary timer tool is **YPT (Yeolpumta)** or native stopwatches.
  - Participants access the web app on desktop monitors and mobile devices during study breaks.

### 1.3 Non-Negotiable Quality Bar
| Metric | Budget / Target | Rationale |
| :--- | :--- | :--- |
| **Authentication Latency** | < 1.5s (Discord OAuth) | Zero password setup friction for Discord community members |
| **Leaderboard Render** | < 400ms (P95) | Competitive tension requires instant, snappy page loads |
| **CSV Import Processing** | < 3.0s for 500 rows | Hosts should never wait or see timeout screens during bulk uploads |
| **Mobile Responsiveness** | 100% viewport compliance (360px–1440px) | Grinders check standings on mobile phones during breaks |
| **Adherence Feedback** | Zero-shame accountability | Emphasize streaks and redemption over public humiliation |

---

## 2. Product Laws & Competitive Positioning

### 2.1 Foundational Product Laws
- **Law L1 (Single Entity Unity):** Solo, Duo, and Squad battles share the exact same underlying team data model ($N=1$, $N=2$, $N \ge 3$). Never create disjoint systems for different game modes.
- **Law L2 (The Spreadsheet Exorcism):** If an admin ever has to open Google Sheets or calculate a formula manually to determine a winner, loser, or punishment, the platform has failed.
- **Law L3 (Forgiving Gamification):** Pure punitive systems cause high churn (60%+ dropouts after week 1). The system must incorporate Grace Passes (buffer days) and clear redemption flows.
- **Law L4 (Discord Identity Primacy):** The user's Discord handle, avatar, and server identity are first-class citizens. No local passwords, no email verification emails.
- **Law L5 (Admin Override Absolute):** Real-world study logs are messy (typos, forgotten timers, app crashes). Admins must have frictionless inline edit power to override any logged record.
- **Law L6 (Explicit Zero-State & Error Design):** Every screen must explicitly define its Loading, Empty, and Error states before any presentation code is signed off.

### 2.2 Competitive Positioning ("Why We Win")
| Competitor / Current System | Competitor Failure Mode | HoldMeToIt Specific Moat |
| :--- | :--- | :--- |
| **Google Sheets + Discord** | Formula breakages, high manual labor, accidental sheet overwrites, detached chat. | Instant automated calculation, Discord OAuth, one-click Webhook broadcast. |
| **YPT (Yeolpumta) In-App Groups** | No team vs team duels, no custom punishment lifecycle, rigid group rules, poor desktop UI. | Multi-mode battles (Duos, Squads), punishment resolution pipelines, custom target configurations. |
| **Generic Habit Trackers (Habitica, Forest)** | Lack cohort/season structure, lack Discord server integration, lack host-driven admin panels. | Purpose-built for community admins running seasonal challenges with cohorts and rosters. |

---

## 3. Phase Legend & Promotion Rule

### 3.1 Phase Tags
- `[P0]`: **MVP Core (Spreadsheet Killer)** — Non-negotiable scope for release 1.0. Must ship.
- `[P1]`: **Operational Polish & Automation** — Matchmaking, interactive Discord Bot, to-do board, recurring cycles.
- `[V1.1]`: **Post-Launch Delight** — Custom badges, streak saver freeze mechanics, PDF/Image export of summary cards.
- `[V2]`: **Ecosystem Independence** — Native web Pomodoro study timer with tab-blur anti-cheat, live 1v1 study arenas.
- `[PROPOSED]`: Feature under consideration; requires group consensus and specification before inclusion.

### 3.2 Promotion Rule
A feature marked `[PROPOSED]` cannot enter active development until:
1. It is documented in the Proposals Ledger (§10).
2. It receives user sign-off and phase re-tagging (`[P0]` or `[P1]`).
3. Its schema and route impacts are reflected in `ARCHITECTURE.md` and `EXECUTION_PLAN.md`.

---

## 4. Complete Screen Map

```text
HoldMeToIt Web Platform
├── 1. Public & Auth
│   ├── Landing Page / Welcome [P0]
│   ├── Discord OAuth Callback (`/auth/callback`) [P0]
│   └── Access Denied / Not Whitelisted [P0]
│
├── 2. Participant Experience (`/dashboard`)
│   ├── Personal Overview Dashboard [P0]
│   │   ├── Target Hours Progress Ring [P0]
│   │   ├── Daily Study Hours Bar Chart [P0]
│   │   ├── Streak Counter & Grace Pass Status [P0]
│   │   └── Daily Study Log Notes Input [P0]
│   ├── Challenge Hub (`/challenge/:id`) [P0]
│   │   ├── Challenge Status & Rules Header [P0]
│   │   ├── Global Leaderboard (Solo / Team Tabs) [P0]
│   │   ├── Team Roster & Teammate Breakdown [P0]
│   │   └── Punishment Ledger & Wall of Accountability [P0]
│   ├── Daily Goal & To-Do Board (`/challenge/:id/todos`) [P1]
│   └── Profile & Past Seasons Archive (`/profile`) [P1]
│
├── 3. Admin / Organizer Suite (`/admin`)
│   ├── Admin Overview & Active Challenges (`/admin`) [P0]
│   ├── Challenge Creator Wizard (`/admin/challenges/new`) [P0]
│   │   ├── Mode Selector (Solo, Duo, Squad) [P0]
│   │   ├── Targets & Cycle Configuration [P0]
│   │   └── Roster Upload / Roster Builder [P0]
│   ├── Challenge Management Console (`/admin/challenges/:id`) [P0]
│   │   ├── Bulk CSV Ingestion Modal (`/admin/challenges/:id/import`) [P0]
│   │   │   ├── File Dropzone & Column Mapper [P0]
│   │   │   ├── Ingestion Preview & Sanity Check Table [P0]
│   │   │   └── Commit Ingestion Action [P0]
│   │   ├── Roster & Team Editor (Drag-and-drop or manual assign) [P0]
│   │   ├── Automated Matchmaking & Balancing Modal [P1]
│   │   ├── Manual Hours Override Table [P0]
│   │   ├── Punishment Status & Clearance Modal [P0]
│   │   └── Discord Webhook Broadcast Trigger [P0]
│   └── Recurring Cycle Scheduler (`/admin/cycles`) [P1]
```

---

## 5. Detailed Feature Specifications: Public & Authentication

### §5.1 Discord OAuth Flow `[P0]`
- **Route:** `/api/auth/signin/discord` $\rightarrow$ `/auth/callback`
- **Purpose:** Frictionless single-click login using existing Discord credentials.
- **Entry Points:** Top navigation bar "Login with Discord" CTA, or landing page hero button.
- **Data & Invariants:**
  - Queries user's Discord ID, Discord username, global display name, and avatar hash.
  - Automatically associates or provisions user in the local `User` table.
  - Assigns default role (`PARTICIPANT`) or promotes to (`ADMIN`) based on server configuration.
- **Designed States:**
  - **Loading:** Discord animated spinner with copy: *"Connecting to Discord..."*
  - **Error:** Clean alert modal: *"Authentication cancelled or failed. Please try again."*

---

## 6. Detailed Feature Specifications: Participant Experience

### §6.1 Personal Overview Dashboard `[P0]`
- **Route:** `/dashboard`
- **Purpose:** Grinder's personal cockpit showing daily/weekly target progress, remaining hours, active streaks, and quick study notes.
- **Layout & Visual Hierarchy:**
  - **Hero Stats Ribbon:** 
    - Active Challenge Name + Days Remaining.
    - Weekly Target Hours Gauge (e.g. `28.5 / 35.0 hrs · 81%`).
    - Current Active Streak (Flame icon + streak days) + Grace Passes remaining (e.g. `1 / 2 Freezes left`).
  - **Visual Chart:** 7-day study hour distribution bar chart comparing actuals vs daily baseline target.
  - **Daily Notes / Quick Log Box:** Lightweight input allowing participant to attach daily subject notes (e.g. *"Completed 4 chapters of Organic Chem"*).
  - **Teammate Glance Widget (Duo/Team mode):** Mini avatar cards showing duo partner's or teammates' hours for the day.
- **Designed States:**
  - **Loading:** Glass-morphism skeleton cards.
  - **Empty:** *"You are not enrolled in an active challenge. View open challenges or contact your server host."*

### §6.2 Challenge Hub & Leaderboard `[P0]`
- **Route:** `/challenge/:id`
- **Purpose:** Real-time competitive leaderboard, team standings, and punishment visibility.
- **Layout & Visual Hierarchy:**
  - **Leaderboard Header:** Toggle between **Team Standings** and **Individual MVPs**.
  - **Podium Display:** Top 3 spots rendered in gold/silver/bronze highlight cards with team badges and cumulative hours.
  - **Rankings Table:** Ranked list with Rank, Member/Team Name, Daily Average, Total Hours Logged, Target Delta (+/- hours), and Status Badge (`On Track`, `In Danger`, `Grace Used`).
  - **The Accountability Ledger (Wall of Flagged Penalties):** Filterable bottom panel listing participants who missed weekly targets or breached minimum thresholds, their assigned punishment, and current status (`FLAGGED`, `PROOF_SUBMITTED`, `RESOLVED`).
- **Data Invariants:**
  - Read-optimized cached leaderboard queries recalculated on every CSV ingestion or manual override.
- **Designed States:**
  - **Empty:** *"Challenge has just begun! Log your hours to claim the #1 spot."*

---

## 7. Detailed Feature Specifications: Admin / Organizer Suite

### §7.1 Challenge Creator Wizard `[P0]`
- **Route:** `/admin/challenges/new`
- **Purpose:** Allow host to launch a new challenge season in under 3 minutes.
- **Form Steps (Wizard):**
  1. **Basics:** Challenge Title, Start Date, End Date, Description.
  2. **Mode & Structure:**
     - Select Mode: Solo ($N=1$), Duos ($N=2$), or Squad Battles ($N=4\text{–}8$).
     - Grace Days: Number of allowed missed/buffer days per cycle (default: 1/week).
  3. **Targets & Rules:**
     - Target Hours per Week (e.g., 35 hrs/week) or Daily Minimum (e.g., 4 hrs/day).
     - Punishment Rules: Define text description of penalty (e.g., *"Post 1-hour study timelapse to Discord"*).
  4. **Discord Webhook Configuration:**
     - Input server webhook URL for automated standings broadcasts.
- **Persistence:** Creates record in `Challenge` table with status `UPCOMING` or `ACTIVE`.

### §7.2 Bulk CSV Ingestion Console `[P0]`
- **Route:** `/admin/challenges/:id/import`
- **Purpose:** Ingest study logs exported from YPT or logged rosters in bulk without manual typing.
- **Workflow:**
  1. **Upload:** Drag-and-drop `.csv` file.
  2. **Parsing & Auto-Mapping:** System parses columns: Participant Name/Identifier, Date, Duration (hours/minutes).
  3. **Sanity Preview Table:**
     - Rows with recognized users are marked with green badges.
     - Unrecognized or misspelled names show a yellow warning dropdown to map to existing enrolled users.
     - Extreme anomalies (>18 hrs/day) flagged with caution badges.
  4. **Commit Button:** Atomic batch insert into `StudyLog` table; recalculates streaks and leaderboards immediately.
- **Designed States:**
  - **Error:** *"Malformed CSV. Expected headers: Username/Email, Date, Hours/Minutes. Download template here."*

### §7.3 Manual Hours Override Table `[P0]`
- **Route:** `/admin/challenges/:id/roster`
- **Purpose:** Admin quick-edit console to correct missed logs, app crashes, or participant disputes inline.
- **Layout:**
  - Paginated data grid of all participants.
  - Inline editable hours cell with instant saving.
  - Audit trail tooltip: Displays who edited the hours and original CSV timestamp.

### §7.4 Punishment Clearance Modal `[P0]`
- **Route:** `/admin/challenges/:id/punishments`
- **Purpose:** Manage, verify, and resolve member punishments.
- **Features:**
  - List of all members currently `FLAGGED`.
  - Actions: **Approve Proof** (sets status to `RESOLVED`), **Grant Host Pardon / Buffer** (sets status to `EXCUSED`), or **Flag for Server Punishment PFP** (triggers webhook alert).

### §7.5 Discord Webhook Standings Broadcast `[P0]`
- **Route:** `/admin/challenges/:id` (Trigger button)
- **Purpose:** Push rich formatted Discord Embed to community server channel with a single click.
- **Embed Content:**
  - Challenge Name, Current Day / Total Days.
  - Top 3 Leaderboard Podium.
  - "Grinder of the Day" / Highest study hours.
  - Flagged Punishment Watchlist.
  - Direct link back to Web Dashboard.

---

## 8. Detailed Feature Specifications: Phase 1 (P1) Enhancements

### §8.1 Automated Matchmaking Engine `[P1]`
- **Route:** `/admin/challenges/:id/matchmaking`
- **Description:** Algorithmic team balancing based on target study hours or previous season performance to avoid one-sided "super-teams".

### §8.2 Interactive Discord Bot Commands `[P1]`
- **Description:** Standalone Node/Python bot service offering `/leaderboard`, `/stats`, `/log`, and automated midnight role changes.

### §8.3 Daily Goal & To-Do Board `[P1]`
- **Route:** `/challenge/:id/todos`
- **Description:** Interactive task board where participants set 3 core daily priorities and check them off alongside logged study hours.

### §8.4 Recurring Cycle Scheduling `[P1]`
- **Route:** `/admin/cycles`
- **Description:** Automated season rotation (e.g., 2-Week Duo Battle $\rightarrow$ 3-Day Break $\rightarrow$ 2-Week Squad Battle) with historical archiving.

---

## 9. Detailed Feature Specifications: Phase 2 (V2) Future Horizon

### §9.1 Native Live Study Timer (Pomodoro / Stopwatch) `[V2]`
- In-browser study timer syncing directly with personal logs. Includes window focus/tab blur detection to discourage multitasking.

### §9.2 XP, Badges & Tier Progression `[V2]`
- Long-term gamification system granting permanent profile badges (e.g., *"Centurion: 100 Hours Logged"*, *"Iron Will: 14-Day Streak"*) surviving across seasonal wipes.

---

## 10. Proposals Ledger

| ID | Feature Name | Target Phase | Proposed By | Status | Description & Strategic Value |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **PROP-01** | Discord Role Syncing | `[P1]` | Architecture | `PROPOSED` | Auto-assign `@On-Track` and `@In-Punishment` roles via Discord Bot. |
| **PROP-02** | Shareable Social Cards | `[P1]` | Product | `PROPOSED` | Dynamic OG image generator rendering participant weekly stats card for Instagram/Discord sharing. |
| **PROP-03** | Spotify Study Session Embed | `[V2]` | Product | `PROPOSED` | Embedded Lofi/Ambient study playlist inside the dashboard view. |
