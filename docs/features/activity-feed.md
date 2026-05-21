---
title: "Activity Feed"
slug: "activity-feed"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-21"
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
- **Retainer summary bar** at the top shows combined retainer budget, hours logged, hours remaining, and client count across all sites with [Retainer Tracking](client-profile/retainer-tracking.md) configured. Includes an achievements banner with gamification milestones (completion badges, streak tiers, personal bests). See [Retainer Tracking — Agency-Wide Summary](client-profile/retainer-tracking.md#agency-wide-summary-activity-feed) for details.
- **Summary stats bar** shows 7-day activity counts across five categories for quick situational awareness.
- **Search** across entry titles and descriptions to find specific activity.
- Supports filtering by **site**, **category**, **severity**, and **date range** with quick-access date presets.
- Groups entries by date (Today, Yesterday, or the full date) for easy scanning.
- Loads 50 entries at a time with a "Load More" button for pagination.
- **Refresh indicator** shows when data was last loaded, with a manual refresh button.

## Why It Matters

- **Cross-client visibility** — See all client work in one place instead of checking each profile individually.
- **Quick triage** — Filter by severity to surface errors and warnings across all sites at once.
- **Accountability** — Every automated and manual action is tracked with timestamps, categories, and source labels.
- **At-a-glance stats** — The summary bar instantly tells you how active things have been this week.

## How to Use It

1. Click **Activity Feed** in the left sidebar under **Tools**.
2. The feed loads with all activity across all your sites, newest first.
3. Review the **summary stats bar** at the top for a 7-day snapshot (Content, Manual, Automation, SEO, Errors).
4. Use the **search box** (top right) to find specific entries by keyword.
5. Use the **Site** filter buttons to narrow to a specific client.
6. Use **Category** filters (Content, Automation, Site, SEO, System, Manual) to focus on a type of work.
7. Use **Severity** filters (Success, Warning, Error, Info) to surface issues.
8. Use **date presets** (Today, Last 7 Days, Last 30 Days) for quick time ranges, or the custom date pickers for specific windows.
9. Click a **site badge** on any entry to jump to that client's full Activity & Logs tab.
10. Use the **refresh button** (sync icon, top right of timeline) to reload the latest data.

## Summary Stats Bar

Five stat cards displayed at the top of the page, each showing a count for the last 7 days:

| Card | What It Counts |
|------|---------------|
| **Content** | Content creation and publishing events |
| **Manual** | Manual work entries (phone calls, meetings, etc.) |
| **Automation** | Automated jobs and scheduled tasks |
| **SEO** | SEO analyses, scans, and audits |
| **Errors** | Entries with error severity across all categories |

Stats update when you change the site filter, so you can see per-client breakdowns.

## Filters

| Filter | Options | Description |
|--------|---------|-------------|
| Search | Free text | Searches entry titles and descriptions |
| Site | All Sites, or individual site buttons | Show activity for one or all clients |
| Category | All, Content, Automation, Site, SEO, System, Manual | Filter by event type |
| Severity | All, Success, Warning, Error, Info | Filter by importance level |
| Date Presets | Today, Last 7 Days, Last 30 Days | One-click date range shortcuts |
| Date Range | From / To date pickers | Custom time window |

## Refresh Indicator

A subtle status line above the timeline shows when data was last fetched:

- **"Updated just now"** — immediately after loading.
- **"Updated Xm ago"** — updates every 30 seconds so you know how stale the data is.
- Click the **sync icon** to manually refresh both the timeline and the summary stats. The icon spins while loading.

## Relationship to Per-Site Activity & Logs

The Activity Feed and the per-site Activity & Logs tab read from the **same data source** (`activity_log` table). The difference is scope:

| Feature | Scope | Location |
|---------|-------|----------|
| **Activity & Logs** (per-site) | Single client | Client Profile → Activity & Logs tab |
| **Activity Feed** (global) | All clients combined | Sidebar → Tools → Activity Feed |

The per-site tab also includes features not available on the global feed: the Work Log dashboard (with timer), Client Report Builder, Full Log table with CSV export, and manual work entry editing.

## Notes / Edge Cases

- The Activity Feed only shows activity for sites owned by the logged-in user. Users cannot see other users' site activity.
- Manual work entries display duration badges (e.g., "2h 30m") just like in the per-site view.
- Post titles are clickable and link to the post detail page.
- Activity older than 90 days is automatically cleaned up by the system's daily maintenance job.
- Search is case-insensitive and matches partial words (e.g., searching "blog" will match "Blog post published").
- The summary stats bar fetches up to 500 entries for the 7-day window to compute counts. For accounts with extremely high activity, counts may be approximate.
