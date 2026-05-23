---
title: "Retainer Gamification & Milestones"
slug: "retainer-gamification"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Retainer Gamification & Milestones

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

An achievements and rewards system layered on top of retainer tracking. Milestones, streaks, and personal bests appear automatically based on your work patterns, turning budget tracking into a motivational feedback loop.

## Where It Appears

The **Activity Feed** page (`/activity-feed`) shows a combined retainer summary bar at the top. The achievements banner sits within this summary, displaying earned milestones as colored chips and badges.

## Quota Milestones

| Milestone | Trigger | Visual |
|-----------|---------|--------|
| Halfway | Client reaches 50% of quota | Blue chip with percentage |
| Quota Met | Client reaches 100% (within 10% overage) | Green chip with checkmark |
| Over Quota | Client exceeds quota by more than 10% | Orange chip with fire icon and overage amount |
| Finished Early | Quota met with 5+ days remaining in the period | Lightning bolt icon on the chip |
| All Clients Touched | Every client has at least some hours logged | Purple chip |
| Perfect Month | Every client meets quota in the same period | Gold crown banner across the top of the section |

## Streak Tiers

Streaks count consecutive closed periods where quota was met. They appear as colored fire chips per client.

| Tier | Requirement | Color |
|------|-------------|-------|
| Bronze | 3 consecutive periods | Bronze |
| Silver | 6 consecutive periods | Silver |
| Gold | 12 consecutive periods | Gold |

## Personal Bests

| Milestone | Trigger | Visual |
|-----------|---------|--------|
| Personal Best | Total hours this period exceeds all previous periods | Yellow star chip |
| Record Delivered | More clients delivered than any prior period | Yellow medal chip |

Streaks and personal bests require closing periods to build history. They will appear once billing cycles are closed using the Close Period button on individual site retainer trackers.

## Per-Client Breakdown

Click **Per-client breakdown** to expand a grid showing each client's logged hours, quota, remaining hours, completion badge, and streak count.
