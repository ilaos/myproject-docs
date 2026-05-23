---
title: "Retainer Settings Change Log"
slug: "retainer-settings-log"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: "CP-RETAINER-LOG"
last_updated: "2026-05-23"
---

# Retainer Settings Change Log

**Tier:** Pro/Agency | **Type:** Background

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

A background audit trail that automatically records every change to retainer settings and work schedule preferences. Captures old and new values with timestamps so pacing shifts can be traced back to a specific configuration change.

## Why It Matters

When retainer hours, billing cycles, or work schedule preferences change, the daily target and pacing calculations shift immediately. Without a change log, a sudden spike in required pace could appear unexplained. This table provides the context to understand why pacing changed on a specific date.

## What It Logs

### Retainer Settings (per site)

Logged when saving retainer settings via the gear icon on the Activity Logs tab.

| Setting | Example Change |
|---------|---------------|
| `retainer_hours` | 10 -> 16 |
| `billing_cycle_day` | 1 -> 15 |
| `show_hours_in_reports` | 0 -> 1 |

### Work Schedule Preferences (per user)

Logged when saving work schedule preferences via the calendar icon on the Activity Logs tab.

| Setting | Example Change |
|---------|---------------|
| `include_weekends` | 0 -> 1 |
| `timezone` | America/New_York -> America/Chicago |
| `workday_end_hour` | 21 -> 18 |

## Database

| Column | Type | Description |
|--------|------|-------------|
| `id` | INTEGER | Auto-incrementing primary key |
| `user_id` | INTEGER | User who made the change |
| `site_id` | INTEGER | Site affected (NULL for user-level settings like timezone) |
| `setting_name` | TEXT | Name of the setting that changed |
| `old_value` | TEXT | Previous value (as string) |
| `new_value` | TEXT | New value (as string) |
| `changed_at` | TIMESTAMP | When the change occurred |

## Current State

**Data capture only.** Changes are logged automatically but there is no UI to view the log. The data can be queried directly:

```sql
SELECT * FROM retainer_settings_log ORDER BY changed_at DESC;
```

Future use cases include annotating pacing charts and intelligence slides to explain why targets shifted on a specific date.

## Notes / Edge Cases

- Only actual changes are logged. If a user saves settings without modifying any values, no rows are written.
- User-level settings (work schedule) have `site_id = NULL` since they apply across all clients.
- The table is created at server startup and has no foreign key constraints for simplicity.
