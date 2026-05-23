---
title: "Client Retainer Intelligence & Tracking"
slug: "retainer-tracking"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Client Retainer Intelligence & Tracking

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    This isn't just an hours counter. Client Retainer Intelligence & Tracking is a full operational command center that combines budget tracking, real-time timers, gamification, daily pacing briefings, and predictive work intelligence. It answers not only "how many hours do I have left?" but also "am I heading for a crunch?", "which clients are eating my time?", and "am I ahead or behind last month?"

## Overview

Per-site monthly hour quota tracking with custom billing cycles, pace indicators, overage rollover, period history, work timers, gamification milestones, daily pacing briefings, and a global intelligence layer that analyzes patterns across all clients. Lives at the top of the Activity & Logs tab in Client Profile, with cross-site intelligence surfaced in the topbar stats ticker on every page.

## Why It Matters

Most SEO and marketing agencies operate on retainer models where clients pay for a set number of hours per month. Without tracking, agencies either over-service clients (losing money) or under-service them (risking churn). This feature provides real-time visibility into budget utilization per client, plus the operational intelligence to manage workload, pace, and sustainability across your entire portfolio.

## Sub-Features

| Feature | What It Does |
|---------|-------------|
| **[Retainer Tracking (Core)](retainer-tracking-core.md)** | Per-site hour budgets, billing cycles, progress bars, pace indicators, rollover, period history |
| **[Retainer Gamification & Milestones](retainer-gamification.md)** | Quota milestones, streak tiers, personal bests, achievements banner |
| **[Work Timer & Topbar Indicator](work-timer.md)** | Real-time per-client stopwatch with topbar display for up to 3 concurrent timers |
| **[Work Schedule Preferences](work-schedule-preferences.md)** | Weekend toggle, timezone auto-detection, workday end hour |
| **[Daily Pacing Briefing](daily-pacing-briefing.md)** | Personalized login modal with daily target, gap reduction scenarios, burnout alerts |
| **[Work Intelligence](work-intelligence.md)** | Compression detection, momentum tracking, client silence alerts, time sink detection, work category breakdown |
| **[Retainer Settings Change Log](retainer-settings-log.md)** | Background audit trail for all retainer and work schedule setting changes |

## How to Use It

### Initial Setup

1. Go to any site's **Activity / Logs / Reports** tab.
2. The Retainer Tracker section appears at the top. If not yet configured, you'll see a setup card.
3. Enter the **Monthly Hours** (e.g., 16) and **Billing Day** (1-31, the day the client's billing period starts).
4. Optionally toggle **Include hours in client reports** to show hours in emailed work reports.
5. Click **Enable Retainer Tracking**.

### Day-to-Day Use

Once configured for at least one site, the system activates across the platform:

- **Activity Logs tab** — Retainer tracker with progress bar, hours, pace, and timer
- **Topbar (every page)** — Stats ticker carousel with daily target, tier breakdown, and intelligence slides
- **Login** — Daily Pacing Briefing modal with personalized action plan
- **Topbar timer pills** — Up to 3 concurrent client timers visible from any page

### Data Source

Retainer hours are calculated from **all activity log entries with a duration** — manual work entries, automated entries with time added, and timer-logged sessions. The system uses `json_extract(metadata, '$.duration_minutes') > 0` to count any entry where time was recorded.

## Key Settings

| Setting | Range | Description |
|---------|-------|-------------|
| Monthly Hours | 0.5 - 744 | Hour quota per billing period |
| Billing Day | 1 - 31 | Day of month the billing period starts |
| Show in Reports | On/Off | Include hours summary in client work report emails |
| Include Weekends | On/Off | Count Sat/Sun as available workdays for pacing calculations |
| Timezone | Auto-detected | Used for "today" calculation and workday hour boundaries |
| Workday End Hour | 1-23 | When your workday ends (for reachability calculations) |

## Billing Period Calculation

The billing period is defined by the Billing Day setting:

| Billing Day | Today | Period |
|-------------|-------|--------|
| 17 | May 20 | May 17 - Jun 16 |
| 17 | May 10 | Apr 17 - May 16 |
| 1 | May 20 | May 1 - May 31 |
| 30 | Feb 15 | Jan 30 - Feb 27 |

## Rollover Logic

- **Over quota:** Extra hours can be rolled forward (reduces next month's workload) or written off (next month starts fresh).
- **Under quota:** Unused hours always expire. The client is not owed makeup hours.
- **Rollover display:** When rollover exists, a notice appears: "1.5h carried from last period - effective budget: 14.5h".

## Database

| Table/Column | Purpose |
|-------------|---------|
| `sites.retainer_hours` | Monthly hour quota (nullable) |
| `sites.billing_cycle_day` | Day of month billing starts (nullable, 1-31) |
| `sites.show_hours_in_reports` | Whether to include hours in client reports |
| `users.include_weekends` | Whether weekends count as workdays |
| `users.timezone` | User's timezone for date calculations |
| `users.workday_end_hour` | Hour (0-23) when the workday ends |
| `retainer_periods` | Closed period snapshots (site_id, period dates, quota, logged minutes, rollover minutes, closed_at) |

## API Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/retainer/settings` | Get retainer settings for a site |
| POST | `/api/retainer/settings` | Save retainer settings |
| GET | `/api/retainer/status` | Get current period status, hours, pace, and history |
| POST | `/api/retainer/close-period` | Close current period with rollover or write-off |
| GET | `/api/work-schedule` | Get user work schedule preferences |
| POST | `/api/work-schedule` | Save user work schedule preferences |
| GET | `/api/burnout-check` | Get daily target, tier breakdown, intelligence slides, burnout alerts |

## Agency-Wide Summary (Activity Feed)

The cross-site **Activity Feed** page (`/activity-feed`) shows a combined retainer summary bar at the top, aggregating all clients with retainer tracking configured. It displays total budget, total hours logged, total remaining, client count, and a progress bar.

Click **Per-client breakdown** to expand a grid showing each client's logged hours, quota, remaining hours, completion badge, and streak count.

## Notes / Edge Cases

- Retainer tracking is entirely optional. Sites without it configured see a setup card instead of the tracker.
- Disabling retainer tracking preserves period history in the database.
- The progress bar caps at 100% visually but the percentage and hours remaining continue to reflect the true overage.
- Work report emails use the billing period dates as the header date range when retainer is configured.
- For months shorter than the billing day (e.g., day 30 in February), the system clamps to the last day of that month.
