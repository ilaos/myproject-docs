# Strategy Game Plan

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    Strategy Game Plan is the "what do I need to do for this client and when?" layer. It turns abstract SEO strategies into concrete, recurring operational tasks grouped into phases with strategic context. The check-off system auto-logs to Activity Logs, so completing strategy tasks doubles as work documentation without duplicate entry. Login reminders ensure nothing falls through the cracks even when you're logging in for a different reason.

## Overview

A per-site recurring task scheduler that lives in the Client Profile sidebar under "Strategy Game Plan." It combines three concepts:

1. **Phases** — named groups with descriptions that capture strategic context (the "why"). Each phase has a status: Active, Upcoming, or Completed.
2. **Recurring Tasks** — tasks that repeat on a schedule (weekly, bi-weekly, or monthly) with a specific day of the week.
3. **One-Time Milestones** — deliverables that need to happen once with an optional due date.

The weekly calendar view shows what's due right now. The phase view shows the full strategic picture organized by execution stage.

## Why It Matters

SEO work is inherently recurring and phased. Without a structured plan, it's easy to forget what was promised, miss deadlines, or lose track of where you are in a multi-phase strategy. This feature keeps the SEO practitioner accountable to a defined playbook and provides proof of execution through automatic activity logging.

## Access Control

**Permission Mode:** Per-user, per-site. Each user sees only their own strategy tasks for sites they own.

---

## Core Concepts

### Phases

Phases represent strategic stages of work. A typical engagement might have:

- **Phase 1: Technical Foundation** (Active) — schema deployment, speed optimization, lead capture redesign
- **Phase 2: Content Silos** (Upcoming) — hub/spoke pages, compliance content, E-E-A-T authority building
- **Phase 3: Regional Dominance** (Upcoming) — interlinking, review velocity, geographic expansion

Each phase has:

| Field | Purpose |
|-------|---------|
| **Name** | Short identifier (e.g., "Phase 1: Technical Authority") |
| **Description** | Strategic context — the reasoning, goals, and approach. This is what you read when you come back cold in 3 weeks. |
| **Status** | `Active` (tasks show in weekly view + reminders), `Upcoming` (visible in phase view only), `Completed` (collapsed) |

Only tasks in **Active** phases appear in the weekly view and trigger login reminders.

### Recurring Tasks

Tasks that repeat on a defined cadence:

| Frequency | How It Works |
|-----------|-------------|
| **Weekly** | Due every week on the specified day |
| **Bi-weekly** | Due on weeks 1 & 3 or weeks 2 & 4 of the month |
| **Monthly** | Due on a specific week of the month (week 1, 2, 3, or 4) |

Each task has: title, category, priority (high/medium/low), due day, optional notes, and optional phase assignment.

### One-Time Milestones

Non-recurring deliverables with an optional due date. Examples: "Deploy JSON-LD schema across all city pages," "Redesign above-fold lead capture form."

Milestones:

- Appear with a purple left border and square checkbox
- Show a progress bar: "Milestones: 3/8 done"
- Stay visible after completion (checked off, not hidden)
- Overdue milestones get a red border when past their due date

### On Hold

Individual tasks can be paused without deleting them. On-hold tasks:

- Appear dimmed with a dashed border and yellow "On Hold" badge
- Don't count toward due/overdue statistics
- Don't trigger login reminders
- Can't be checked off (must be resumed first)
- Sort to the bottom of their group

Use case: Task B depends on Task A. Put Task B on hold, complete Task A, then resume Task B.

---

## Views

### Weekly View (default)

Groups recurring tasks by day of the week (Monday through Sunday). Shows:

- Today highlighted with a "TODAY" badge
- Task count per day ("3 this week")
- Overdue tasks (past their due day) with red left border
- Completed tasks (checked off) with green background, sorted to bottom
- One-time milestones in a separate "Milestones" section at the bottom
- Phase pills at the top showing all phases with status indicators (clickable to switch to phase view)

Only tasks in **active phases** (or unphased tasks) appear here.

### Phase View

Groups all tasks by phase. Each phase shows:

- Status dot (green = active, yellow = upcoming, gray = completed)
- Phase name and task count (done/total)
- Collapsible description with strategic context
- All tasks within the phase (sorted by priority)
- "Add Task to Phase" button at the bottom

Completed phases auto-collapse. Upcoming phases appear dimmed.

---

## Statistics

Four stat cards at the top of the page:

| Stat | What It Tracks |
|------|---------------|
| **Total Tasks** | All active tasks across all phases |
| **Due This Week** | Recurring tasks due this specific week (respects frequency rules) |
| **Done This Week** | Tasks completed since Monday |
| **Week Streak** | Consecutive weeks where all due tasks were completed |

A milestones progress bar appears below the stats when milestones exist.

---

## Login Reminders

When you load the `/sites` page (main dashboard), a banner appears if any strategy tasks are due across any of your sites:

> "5 strategy tasks due this week (2 overdue)"

Expandable to show per-site breakdown with task names and links to each site's game plan. On-hold tasks and tasks in non-active phases are excluded.

---

## Activity Log Integration

Every task completion auto-creates an entry in the Activity Logs with:

- Category: `strategy`
- Action: `task_completed`
- Title: "Strategy: [task title]"
- Description: the optional completion note
- Metadata: strategy category, note

This means completed strategy tasks automatically appear in the Activity Timeline and can be included in Client Work Report Emails.

---

## Templates

Four pre-built strategy templates can be loaded with one click:

| Template | Focus | Tasks |
|----------|-------|-------|
| **Local SEO Weekly** | Local business essentials | 5 weekly tasks (blog, reviews, social, GSC, GMB) |
| **E-commerce Monthly** | Online store checklist | 5 monthly tasks across different weeks |
| **Content-Heavy Weekly** | Content marketing cadence | 5 weekly tasks (research, write, publish, link, promote) |
| **Backlink Building Bi-Weekly** | Link building rhythm | 5 bi-weekly/monthly tasks (prospect, outreach, follow-up) |

Templates **add** tasks — they don't replace existing ones. Tasks can be customized after loading.

---

## Data Model

### Tables

**strategy_phases**

| Column | Type | Purpose |
|--------|------|---------|
| id | INTEGER PK | Auto-increment |
| site_id | INTEGER FK | Which site this phase belongs to |
| user_id | INTEGER FK | Who created it |
| name | TEXT | Phase name |
| description | TEXT | Strategic context (nullable) |
| status | TEXT | `active`, `upcoming`, or `completed` |
| display_order | INTEGER | Sort position |

**strategy_tasks**

| Column | Type | Purpose |
|--------|------|---------|
| id | INTEGER PK | Auto-increment |
| site_id | INTEGER FK | Which site |
| user_id | INTEGER FK | Who created it |
| title | TEXT | Task title (max 200 chars) |
| category | TEXT | content, technical_seo, backlinks, local_seo, analytics, social, reporting, other |
| priority | TEXT | high, medium, low |
| frequency | TEXT | weekly, biweekly, monthly, once |
| due_day | TEXT | monday–sunday (for recurring) |
| week_of_month | INTEGER | 1–4 (for monthly/biweekly) |
| biweekly_weeks | TEXT | "1,3" or "2,4" |
| phase_id | INTEGER FK | Optional phase assignment |
| due_date | TEXT | YYYY-MM-DD (for milestones) |
| is_on_hold | INTEGER | 0 or 1 |
| is_active | INTEGER | Soft delete (1 = active) |
| notes | TEXT | Optional details |

**strategy_completions**

| Column | Type | Purpose |
|--------|------|---------|
| id | INTEGER PK | Auto-increment |
| task_id | INTEGER FK | Which task was completed |
| site_id | INTEGER FK | Which site |
| user_id | INTEGER FK | Who completed it |
| note | TEXT | Optional completion note |
| activity_log_id | INTEGER FK | Link to activity_log entry |
| completed_at | TIMESTAMP | When it was completed |

---

## API Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/strategy-tasks?site_id=X` | Get all tasks, phases, completions, and stats |
| POST | `/api/strategy-tasks` | Create a task |
| POST | `/api/strategy-tasks/bulk` | Create multiple tasks (templates) |
| PUT | `/api/strategy-tasks/:id` | Update a task |
| DELETE | `/api/strategy-tasks/:id` | Delete a task |
| POST | `/api/strategy-tasks/:id/complete` | Mark completed (creates activity log) |
| POST | `/api/strategy-tasks/:id/uncomplete` | Undo completion |
| POST | `/api/strategy-tasks/:id/hold` | Toggle on-hold status |
| POST | `/api/strategy-phases` | Create a phase |
| PUT | `/api/strategy-phases/:id` | Update a phase |
| DELETE | `/api/strategy-phases/:id` | Delete a phase (tasks become unphased) |
| GET | `/api/strategy/due-summary` | Cross-site due summary (for login banner) |

---

## Requirements

- **Integrations:** None (standalone feature)
- **Depends On:** Activity Logs (for completion logging), Notifications system (for login reminders)
- **Database:** SQLite (post_schedule.db) — 3 tables

## Files

| File | Purpose |
|------|---------|
| `templates/client_profile/strategy_gameplan.html` | Full UI template (HTML + CSS + JS) |
| `dashboard.py` (strategy section) | All API endpoints and helper functions |
| `db_migrations.py` | Table creation and column additions |
