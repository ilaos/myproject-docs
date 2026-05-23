---
title: "Work Schedule Preferences"
slug: "work-schedule-preferences"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Work Schedule Preferences

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

Per-user settings that control how the retainer system calculates pacing, daily targets, and workday boundaries. These preferences affect every retainer calculation across all clients.

## How to Access

On any client's **Activity / Logs / Reports** tab, click the **calendar icon** button in the Work Log section to open the Work Schedule settings panel.

## Settings

| Setting | Options | Default | Description |
|---------|---------|---------|-------------|
| Include Weekends | On/Off | Off | When enabled, Saturday and Sunday count as available workdays for pacing calculations. Useful if you regularly work weekends. |
| Workday End Hour | 1:00 AM - 11:00 PM | 9:00 PM | The hour your workday ends. Used to calculate whether today's daily target is reachable given the current time. |
| Timezone | All IANA timezones | Auto-detected | Your timezone, used for determining "today" in all pacing calculations. |

## Timezone Auto-Detection

On your first visit, the system detects your browser's timezone using `Intl.DateTimeFormat().resolvedOptions().timeZone` and saves it automatically via `POST /api/work-schedule`. This ensures pacing calculations use the correct local date and time without manual configuration.

## What These Settings Affect

- **Daily target calculation** -- "Remaining hours / workdays left" uses the weekend toggle to determine which days count
- **Workdays remaining** -- Excludes weekends unless the toggle is on
- **"Unreachable today" detection** -- Compares daily target against hours left in the day (current hour vs. workday end hour)
- **Tomorrow's target preview** -- Accounts for whether today counts as a workday
- **Burnout alerts** -- Weekend work frequency detection adjusts based on the weekend toggle
- **Stats ticker slides** -- All tier breakdowns and pacing slides use these preferences

## API

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/work-schedule` | Get current work schedule preferences |
| POST | `/api/work-schedule` | Save work schedule preferences |

## Database

| Column | Table | Type | Description |
|--------|-------|------|-------------|
| `include_weekends` | `users` | Boolean | Whether weekends are workdays |
| `timezone` | `users` | String | IANA timezone identifier |
| `workday_end_hour` | `users` | Integer | Hour (0-23) when the workday ends |
