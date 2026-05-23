---
title: "Retainer Tracking (Core)"
slug: "retainer-tracking-core"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Retainer Tracking (Core)

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

Per-site monthly hour quota tracking with custom billing cycles, pace indicators, overage rollover, and period history. Lives at the top of the Activity & Logs tab in Client Profile, directly above the Work Log section.

## How to Use It

### Setup

1. Go to any site's **Activity / Logs / Reports** tab.
2. The Retainer Tracker section appears at the top. If not yet configured, you'll see a setup card.
3. Enter the **Monthly Hours** and **Billing Day**.
4. Optionally toggle **Include hours in client reports**.
5. Click **Enable Retainer Tracking**.

### Day-to-Day Use

Once configured, the tracker shows:

- **Progress bar** -- Color-coded visualization of hours used vs. quota (green -> blue -> orange -> red as you approach/exceed quota).
- **Hours Logged** -- Total work hours in the current billing period.
- **Hours Remaining** -- How many hours are left. Goes negative (shown in red) when over quota.
- **Days Until Due** -- Countdown to the billing cycle end date.
- **Pace** -- Ahead, On Track, or Behind based on where you should be proportionally through the period.

### Changing Settings

Click the **gear icon** in the Retainer Tracker header to open an inline settings panel. You can adjust hours, billing day, and report visibility, or click the red X to disable retainer tracking (history is preserved).

### Closing a Period

At the end of each billing cycle, click **Close Period**. A modal shows:

- Period summary (dates, quota, hours logged, over/under amount)
- **If over quota**, two options:
    - **Roll forward** -- Overage hours carry into the next period as a credit, reducing next month's required work.
    - **Write off** -- Overage is recorded in history but does not carry forward. Next period starts fresh.
- **If under quota** -- Unused hours do not carry forward.

### Period History

Click **Period History** below the tracker to see a collapsible table of the last 6 closed periods, showing quota, logged hours, over/under, and any rolled-forward hours.

## Data Source

Hours are calculated from all activity log entries with a duration -- manual work entries, automated entries with time added, and timer-logged sessions. The query uses `json_extract(metadata, '$.duration_minutes') > 0` to count any entry where time was recorded, regardless of category.

## Notes / Edge Cases

- Retainer tracking is entirely optional. Sites without it configured see a setup card instead of the tracker.
- Disabling retainer tracking preserves period history in the database.
- The progress bar caps at 100% visually but the percentage and hours remaining continue to reflect the true overage.
- Work report emails use the billing period dates as the header date range when retainer is configured.
