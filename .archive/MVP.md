# HoldMeToIt — MVP Feature & Requirements Breakdown

> **Status:** MVP Baseline Specification  
> **Target Delivery:** 2–3 Weeks (3–4 Developers)  
> **Tech Stack:** *Stack-Agnostic (Pending Group Consensus)*  

---

## 1. Objective & Success Metric

- **Mission:** Eliminate "Admin Burnout" and manual Google Sheets management for Discord study battles by automating event creation, self-logging, leaderboard calculations, and punishment enforcement.
- **Core Success Metric:** A host can run an entire week-long study challenge from setup to punishment enforcement with **zero Google Sheets** and **zero manual formula calculation**.

---

## 2. User Roles & Access

| Role | Access Level | Core Actions |
| :--- | :--- | :--- |
| **Spectator / Guest** | Public Read-Only | View match scoreboard, standings, and download punishment PFP. |
| **Participant** | Authenticated User | Declare target hours and goals (pre-event), self-log daily hours (`HH:MM:SS`), check off tasks. |
| **Admin / Host** | Full Control | Create challenges, assign teams, edit/override hours, unlock goals, lock final results, generate Discord announcements. |

---

## 3. Challenge Formats & Core Rules

1. **Formats Supported:**
   - **Team vs Team:** Two balanced rosters (e.g. *Bees vs Butterflies*).
   - **Duos ($N=2$):** Two-person accountability pairs.
   - **Free-for-All ($N=1$):** Individual server-wide leaderboard.
2. **Scoring:** Cumulative total study hours logged during the event window.
3. **No Grace Days (Catch-Up Model):** Missed hours on any day can be compensated on remaining days. A dynamic deficit tracker calculates the required daily pace to stay on track.
4. **Punishment Trigger:** Auto-flagged if a participant fails **either**:
   - Total logged hours < Declared target hours.
   - Any mandatory weekly to-do goal remains uncompleted.
5. **Punishment Asset:** Direct web download button for the server's **Punishment PFP**. Host has manual override power to pardon/excuse emergencies.

---

## 4. MVP Feature Breakdown

```
HoldMeToIt MVP
├── 1. Authentication & Identity
│   ├── Discord OAuth Login (Discord ID, username, avatar)
│   └── Public Spectator Mode (no login required to view)
│
├── 2. Admin Challenge Operations
│   ├── Event Creator (Title, Start/End timestamps, Mode, Team Roster)
│   ├── Manual Override Grid (Edit any logged hours or goal state)
│   ├── Challenge Finalize & Lock (Freezes all participant edits)
│   └── 1-Click Discord Summary Generator (Formatted text copied to clipboard)
│
├── 3. Participant Pre-Event Declaration (Locked once event starts)
│   ├── Declared Weekly Study Target (`HH:MM:SS`)
│   └── Mandatory Weekly Goals List (Tasks to check off)
│
├── 4. Daily Logging & Personal Dashboard
│   ├── Clock-Time Input (`HH:MM:SS` for selected day)
│   ├── Weekly Progress Gauge (% completed, hours remaining)
│   ├── Daily Catch-Up Pace Calculator ("Need Xh Ym/day to hit target")
│   └── Interactive Task Checklist (Check off finished goals)
│
└── 5. Live Scoreboard & Standings
    ├── Head-to-Head Banner (Team totals, current leader, lead delta)
    ├── Roster Standings Table (Rank, Member, Hours, Target, Tasks, Status)
    └── Punishment Wall (Flagged list + Download Punishment PFP button)
```

---

## 5. Key Calculations & Business Rules

1. **Clock Precision:** All study times are stored in total seconds and rendered as `HH:MM:SS`.
2. **Locking Rule:** Once the event start time arrives, participant declared targets and task descriptions are permanently locked (editable only via host override).
3. **Deficit Pace Formula:**
   $$\text{Remaining Seconds} = \max(0, \text{Target Seconds} - \text{Logged Seconds})$$
   $$\text{Required Daily Pace} = \frac{\text{Remaining Seconds}}{\text{Days Remaining}}$$
4. **Punishment Validation:**
   $$\text{Flagged} = (\text{Logged Seconds} < \text{Target Seconds}) \lor (\text{Incomplete Tasks} > 0)$$

---

## 6. Strict MVP Non-Goals (Post-MVP)

- ❌ Automated YPT scraper / mobile bot daemon.
- ❌ Automated Discord bot webhooks or slash commands (manual copy-paste text for MVP).
- ❌ In-browser stopwatch / Pomodoro timer anti-cheat.
- ❌ Automated MMR / skill-based matchmaking.
- ❌ Payment / wagering integrations.

---

## 7. Suggested 3–4 Developer Allocation

| Developer | Primary Responsibility Focus |
| :--- | :--- |
| **Dev 1 (Identity & Data)** | Auth flows, core entity schemas, database migrations, challenge lifecycle states. |
| **Dev 2 (Engine & Math)** | Time parsers (`HH:MM:SS`), deficit calculators, punishment validation logic, test suite. |
| **Dev 3 (Participant UI)** | Participant cockpit, `HH:MM:SS` input component, weekly task checklist, progress gauges. |
| **Dev 4 (Admin & Standings)** | Live match banner, leaderboard table, manual override grid, Discord summary generator. |
