---
title: "Retainer Tracking"
slug: "retainer-tracking"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-21"
---

# Retainer Tracking

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    Retainer Tracking turns the Activity & Logs tab from a passive record into an active budget management tool. It answers the question every agency needs: "How many hours do I have left this month for this client?"

## Overview

Per-site monthly hour quota tracking with custom billing cycles, pace indicators, overage rollover, and period history. Lives at the top of the Activity & Logs tab in Client Profile, directly above the Work Log section. Hours are calculated from manual work entries logged in the same tab.

## Why It Matters

Most SEO and marketing agencies operate on retainer models where clients pay for a set number of hours per month. Without tracking, agencies either over-service clients (losing money) or under-service them (risking churn). This feature provides real-time visibility into budget utilization per client.

## How to Use It

### Initial Setup

1. Go to any site's **Activity / Logs / Reports** tab.
2. The Retainer Tracker section appears at the top. If not yet configured, you'll see a setup card.
3. Enter the **Monthly Hours** (e.g., 16) and **Billing Day** (1-31, the day the client's billing period starts).
4. Optionally toggle **Include hours in client reports** to show hours in emailed work reports.
5. Click **Enable Retainer Tracking**.

### Day-to-Day Use

Once configured, the tracker shows:

- **Progress bar** — Color-coded visualization of hours used vs. quota (green -> blue -> orange -> red as you approach/exceed quota).
- **Hours Logged** — Total manual work hours in the current billing period.
- **Hours Remaining** — How many hours are left. Goes negative (shown in red) when over quota.
- **Days Until Due** — Countdown to the billing cycle end date.
- **Pace** — Ahead, On Track, or Behind based on where you should be proportionally through the period.

### Changing Settings

Click the **gear icon** in the Retainer Tracker header to open an inline settings panel. You can adjust hours, billing day, and report visibility, or click the red X to disable retainer tracking (history is preserved).

### Closing a Period

At the end of each billing cycle, click **Close Period**. A modal shows:

- Period summary (dates, quota, hours logged, over/under amount)
- **If over quota**, two options:
    - **Roll forward** — Overage hours carry into the next period as a credit, reducing next month's required work.
    - **Write off** — Overage is recorded in history but does not carry forward. Next period starts fresh.
- **If under quota** — Unused hours do not carry forward.

### Period History

Click **Period History** below the tracker to see a collapsible table of the last 6 closed periods, showing quota, logged hours, over/under, and any rolled-forward hours.

## Key Settings

| Setting | Range | Description |
|---------|-------|-------------|
| Monthly Hours | 0.5 - 744 | Hour quota per billing period |
| Billing Day | 1 - 31 | Day of month the billing period starts. For months shorter than the billing day (e.g., day 30 in February), the system clamps to the last day of that month. |
| Show in Reports | On/Off | Include an hours summary block in client work report emails |

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

## Data Source

Retainer hours are calculated from **manual work entries only** (category = `manual` in the activity log). Automated entries (content generation, audits, etc.) do not count toward the retainer unless you manually add time to them using the duration editor.

## Database

| Table/Column | Purpose |
|-------------|---------|
| `sites.retainer_hours` | Monthly hour quota (nullable) |
| `sites.billing_cycle_day` | Day of month billing starts (nullable, 1-31) |
| `sites.show_hours_in_reports` | Whether to include hours in client reports |
| `retainer_periods` | Closed period snapshots (site_id, period dates, quota, logged minutes, rollover minutes, closed_at) |

## API Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/retainer/settings` | Get retainer settings for a site |
| POST | `/api/retainer/settings` | Save retainer settings |
| GET | `/api/retainer/status` | Get current period status, hours, pace, and history |
| POST | `/api/retainer/close-period` | Close current period with rollover or write-off |

## Agency-Wide Summary (Activity Feed)

The cross-site **Activity Feed** page (`/activity-feed`) shows a combined retainer summary bar at the top, aggregating all clients with retainer tracking configured. It displays total budget, total hours logged, total remaining, client count, and a progress bar.

### Gamification & Milestones

The summary includes an achievements banner that rewards progress with visual chips and badges. Milestones appear automatically based on your work.

#### Quota Milestones

| Milestone | Trigger | Visual |
|-----------|---------|--------|
| Halfway | Client reaches 50% of quota | Blue chip with percentage |
| Quota Met | Client reaches 100% (within 10% overage) | Green chip with checkmark |
| Over Quota | Client exceeds quota by more than 10% | Orange chip with fire icon and overage amount |
| Finished Early | Quota met with 5+ days remaining in the period | Lightning bolt icon on the chip |
| All Clients Touched | Every client has at least some hours logged | Purple chip |
| Perfect Month | Every client meets quota in the same period | Gold crown banner across the top of the section |

#### Streak Tiers

Streaks count consecutive closed periods where quota was met. They appear as colored fire chips per client.

| Tier | Requirement | Color |
|------|-------------|-------|
| Bronze | 3 consecutive periods | Bronze |
| Silver | 6 consecutive periods | Silver |
| Gold | 12 consecutive periods | Gold |

#### Personal Bests

| Milestone | Trigger | Visual |
|-----------|---------|--------|
| Personal Best | Total hours this period exceeds all previous periods | Yellow star chip |
| Record Delivered | More clients delivered than any prior period | Yellow medal chip |

Streaks and personal bests require closing periods to build history. They will appear once billing cycles are closed using the Close Period button on individual site retainer trackers.

### Per-Client Breakdown

Click **Per-client breakdown** to expand a grid showing each client's logged hours, quota, remaining hours, completion badge, and streak count.

## Notes / Edge Cases

- Retainer tracking is entirely optional. Sites without it configured see a setup card instead of the tracker.
- Disabling retainer tracking preserves period history in the database.
- The progress bar caps at 100% visually but the percentage and hours remaining continue to reflect the true overage.
- Work report emails use the billing period dates as the header date range when retainer is configured, instead of the entry date range.
