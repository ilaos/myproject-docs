---
title: "Daily Pacing Briefing"
slug: "daily-pacing-briefing"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Daily Pacing Briefing

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

A personalized modal that appears on login, providing a daily operational briefing with your hour target, pacing status, gap reduction strategies, and burnout alerts. Shows once per browser session.

## What It Shows

The briefing adapts based on your current pacing situation:

### When Today's Target is Reachable

- Time-of-day greeting (Good morning/afternoon/evening)
- **Daily target** in large text -- hours of work needed today to stay on track
- Context stats: remaining hours, workdays left, 7-day average, soonest deadline

### When Today's Target Exceeds Available Hours

- How many hours short you'll be today
- Available work hours remaining (based on workday end hour setting)
- **"Here's the play"** -- shows what happens if you work the remaining hours vs. do nothing:
    - Work X hours today and tomorrow's target drops to Y
    - Do nothing and tomorrow becomes Z
    - Per-hour savings rate (every hour you work saves ~Xh off tomorrow)

### When the Full Quota is Unreachable

- **Projected shortfall** in large text
- Remaining hours vs. max achievable at 8h/day
- **Scenario cards** showing three effort levels:
    - Light (4h/day) -- gap remaining
    - Moderate (6h/day) -- gap remaining
    - Full (8h/day) -- gap remaining or "Gap closed!"
- Each scenario has a progress bar showing percentage of remaining work covered
- **"Right now"** action block -- what to do with whatever time is left today

## Burnout Alerts

Below the pacing data, the briefing surfaces burnout risk alerts when detected:

| Alert | Trigger | Severity |
|-------|---------|----------|
| Heavy streak | 3+ consecutive 8h+ days | Orange (3-4) / Red (5+) |
| Projected heavy days | Current pace requires 3+ consecutive 8h+ days ahead | Orange |
| Unsustainable pace | Daily target 12h+ | Red |
| High intensity | Daily target 10-12h | Orange |
| Elevated pace | Daily target 8-10h | Yellow |
| Weekend erosion | Worked 3 of last 4 weekends | Orange |
| No rest days | Zero days off in last 7 days | Orange/Red |
| Escalating weeks | 3 consecutive weeks of increasing hours (40h+) | Orange |
| End-of-period crunch | Daily target 1.5x+ ideal pace with 5 or fewer workdays left | Yellow |

Each alert includes:

- Severity-colored icon
- Title describing the pattern
- Explanatory message
- Actionable suggestion

When no alerts are triggered, a green "Sustainable pace" message appears instead.

## Severity Levels

The overall briefing header color reflects the worst active alert:

| Level | Meaning | Header Color |
|-------|---------|-------------|
| Green | Healthy, sustainable pace | Green gradient |
| Yellow | Watch, but manageable | Yellow gradient |
| Orange | Elevated, stay aware | Orange gradient |
| Red | Critical, take action | Red gradient |

## Session Behavior

- Shows **once per browser session** (tracked via `sessionStorage`)
- Dismissible via the action button at the bottom
- Action button navigates to `/activity-feed` for the cross-site retainer summary

## Data Source

All data comes from the `/api/burnout-check` endpoint, which aggregates retainer data across all sites with configured billing cycles.
