---
title: "Activity & Logs"
slug: "activity-logs"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-20"
---

# Activity & Logs

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    Activity & Logs is the platform's proof-of-work layer. A single logging utility (log_activity) feeds a filterable timeline (category, severity, date range), with maintenance cleanup and backfill. It also becomes the foundation for client-facing reporting (Work Report Builder) without duplicating "what happened" logic.

## Overview

Unified, per-site timeline inside Client Profile (last tab) that shows everything that happened for a site across content work, SEO analyses, site configuration changes, automation events, and system actions. Replaces the old fragmented approach where users had to check multiple places to understand recent work.

## Why It Matters

Provides a single source of truth for what happened on a site, so users can quickly understand progress, diagnose issues, and report value to clients without hunting across tools.

## Sections

The Activity & Logs tab is split into four sections:

### 1. Retainer Tracker

A per-site monthly hour budget tracker that sits at the top of the tab. Shows progress bar, hours logged/remaining, days until due, and pace indicator. Supports custom billing cycles, overage rollover, period history, work timers, gamification, daily pacing briefings, and a global work intelligence layer. See [Client Retainer Intelligence & Tracking](retainer-tracking.md) for full details.

### 2. Work Log

A dashboard for tracking manual, billable work performed for a client.

- **Stats cards** — Show number of entries and total hours logged this week and this month.
- **"Log New Work" button** — Opens a modal to record manual work entries (phone calls, meetings, research, design work, etc.).
- **Work Timer** — A real-time stopwatch for tracking work as it happens. See [Work Timer & Topbar Indicator](work-timer.md) for full details.
- **Recent Entries** — Quick-glance list of the latest manual entries.

### 3. Activity Timeline & Reports

The main filterable timeline showing all activity for the site.

- **Category filter** — All, Content, Automation, Site, SEO, System, Manual.
- **Severity filter** — All, Success, Warning, Error, Info.
- **Date range filter** — Custom date pickers with Apply/Clear buttons.
- **Client Report Builder** — Select activities via checkboxes and compose a branded email report to send to your client via SendGrid (see [Client Work Report Email](client-work-report-email.md)). Quick-select buttons: **Last 7 Days**, **Last 30 Days**, and **This Billing Period** (visible when retainer is configured).
- **Timeline entries** — Date-grouped cards with icons, category badges, duration badges, source labels, and clickable post titles. Each entry has a **delete button** (X) on hover and automated entries have an **"+ time" button** to add hours/minutes.
- **Load More** — Paginated loading (50 entries per batch).

### 4. Full Log

A tabular view of the complete activity record.

- **Category dropdown filter** and **CSV export** button.
- **Paginated table** with columns: Date, Category, Entry, Type, Duration, and Actions.
- Prev/Next pagination controls.

## Work Timer

A real-time timer for logging work as you do it, instead of estimating after the fact.

### How to Use It

1. In the Work Log section, click **Start Timer**.
2. A live `HH:MM:SS` counter appears with Pause, Stop, and Discard controls.
3. Work on your task — you can navigate away from the page and the timer keeps running.
4. When finished, click **Stop**. The Log Work modal opens with your elapsed time pre-filled (rounded to the nearest 15-minute increment).
5. Fill in the work type, title, and any notes, then save.

### Timer Details

| Behavior | Detail |
|----------|--------|
| Persistence | Timer state is saved in localStorage, so it survives page navigation, tab switches, and browser refresh |
| Scope | Keyed per site — each site has its own independent timer |
| Time increments | Logged in 15-minute increments (rounded to nearest 15 min on stop) |
| Auto-stop cap | Timer automatically stops at **8 hours** to prevent forgotten timers |
| Cap warning | In the last 60 minutes before auto-stop, the hint switches to an orange countdown: "Auto-stops in X mins" |
| Navigation hint | A green message confirms: "Feel free to leave this page — your timer will keep running" |

### Timer Controls

| Control | Action |
|---------|--------|
| **Pause** | Freezes the timer; elapsed time is preserved |
| **Resume** | Resumes the timer from where it was paused |
| **Stop** | Stops the timer and opens the Log Work modal with time pre-filled |
| **Discard** | Cancels the timer after a confirmation prompt |

## Manual Work Entry

When logging work (either via the timer or the "Log New Work" button), you can record:

| Field | Required | Description |
|-------|----------|-------------|
| Work Type | Yes | Phone Call, Client Meeting, Research, SEO, Website Work, DNS/Hosting, Email, Competitor Analysis, Social Media, Design Work, Third-Party Setup, Administrative, Content Planning, Google Ads, or Other |
| Title | Yes | Brief summary of the work (max 200 characters) |
| Description | No | Additional details |
| Date | Yes | When the work was performed (supports date ranges for multi-day work) |
| Time Spent | Yes | Hours and minutes (15-minute increments) |

Manual entries appear in the timeline with a purple left border and work-type-specific icons. They can be edited or deleted after creation.

## Entry Management

All activity entries (manual and automated) support the following actions:

| Action | How | Applies To |
|--------|-----|-----------|
| **Delete** | Click the X button (appears on hover, top-right of entry) | All entries |
| **Edit** | Click the pencil icon to open the edit modal | Manual entries only |
| **Add time** | Click "+ time" button to add hours/minutes via inline popup | Automated entries without a duration |
| **Edit time** | Click the pencil next to the duration badge | Automated entries with existing duration |

Deleting or editing entries automatically refreshes the stats cards, retainer tracker, and full log table.

## Sticky Tab Navigation

When switching between sites using the left sidebar, the current tab is remembered. If you're on the Activity & Logs tab for one client and click another client, you'll land on the same tab for that client instead of defaulting to Overview.

## Access Control

**Permission Mode:** Configurable per client

## Notes / Edge Cases

- Activity older than 90 days is automatically cleaned up by a daily maintenance job.
- Manual work entries are distinguished from automated entries in the timeline with purple styling and a clipboard icon.
- The Client Report Builder only allows selecting "reportable" entries (Content, SEO, Site, Manual categories — not errors).
- Post titles in timeline entries are clickable and link to the post detail page.
