---
title: "Activity Feed"
slug: "activity-feed"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-03-13"
---

# Activity Feed

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    The Activity Feed gives you a single, cross-site view of everything happening across all your clients — no more jumping between individual client profiles to piece together what happened today.

## Overview

The Activity Feed is a global page (`/activity-feed`) that combines activity from every site you manage into one unified, filterable timeline. It pulls from the same activity log data that powers each client's individual Activity & Logs tab, but aggregates it across all sites so you can see the full picture at a glance.

## What It Does

- Displays all logged activity (content creation, automation events, SEO analyses, site changes, manual work entries, and system events) across every site you own in a single timeline.
- Each entry shows a **site badge** identifying which client it belongs to, linking directly to that client's Activity & Logs tab.
- Supports filtering by **site**, **category**, **severity**, and **date range** so you can quickly narrow down what you're looking for.
- Groups entries by date (Today, Yesterday, or the full date) for easy scanning.
- Loads 50 entries at a time with a "Load More" button for pagination.

## Why It Matters

- **Cross-client visibility** — See all client work in one place instead of checking each profile individually.
- **Quick triage** — Filter by severity to surface errors and warnings across all sites at once.
- **Accountability** — Every automated and manual action is tracked with timestamps, categories, and source labels.

## How to Use It

1. Click **More** in the top navigation bar, then select **Activity Feed**.
2. The feed loads with all activity across all your sites, newest first.
3. Use the **Site** filter buttons to narrow to a specific client.
4. Use **Category** filters (Content, Automation, Site, SEO, System, Manual) to focus on a type of work.
5. Use **Severity** filters (Success, Warning, Error, Info) to surface issues.
6. Use the **Date** range picker to look at a specific time window.
7. Click a **site badge** on any entry to jump to that client's full Activity & Logs tab.

## Filters

| Filter | Options | Description |
|--------|---------|-------------|
| Site | All Sites, or individual site buttons | Show activity for one or all clients |
| Category | All, Content, Automation, Site, SEO, System, Manual | Filter by event type |
| Severity | All, Success, Warning, Error, Info | Filter by importance level |
| Date Range | From / To date pickers | Restrict to a time window |

## Relationship to Per-Site Activity & Logs

The Activity Feed and the per-site Activity & Logs tab read from the **same data source** (`activity_log` table). The difference is scope:

| Feature | Scope | Location |
|---------|-------|----------|
| **Activity & Logs** (per-site) | Single client | Client Profile → Activity & Logs tab |
| **Activity Feed** (global) | All clients combined | Top nav → More → Activity Feed |

The per-site tab also includes features not available on the global feed: the Work Log dashboard, Client Report Builder, Full Log table with CSV export, and manual work entry editing.

## Notes / Edge Cases

- The Activity Feed only shows activity for sites owned by the logged-in user. Users cannot see other users' site activity.
- Manual work entries display duration badges (e.g., "2h 30m") just like in the per-site view.
- Post titles are clickable and link to the post detail page.
- Activity older than 90 days is automatically cleaned up by the system's daily maintenance job.
