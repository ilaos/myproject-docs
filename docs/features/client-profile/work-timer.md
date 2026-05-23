---
title: "Work Timer & Topbar Indicator"
slug: "work-timer"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Work Timer & Topbar Indicator

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

A real-time per-client stopwatch for logging work as it happens, with a persistent topbar indicator that keeps timers visible from any page. Supports up to 3 concurrent timers across different clients.

## How to Use It

1. In any client's Activity & Logs tab, find the Work Log section and click **Start Timer**.
2. A live `HH:MM:SS` counter appears with Pause, Stop, and Discard controls.
3. Work on your task -- you can navigate to any page and the timer keeps running.
4. A **purple pill** appears in the topbar header showing the running timer with the client name.
5. When finished, click **Stop** (either in the Activity Logs tab or by clicking the topbar pill to navigate back). The Log Work modal opens with your elapsed time pre-filled (rounded to the nearest 15-minute increment).
6. Fill in the work type, title, and any notes, then save. The timer state is cleared only after a successful save.

## Timer Behavior

| Behavior | Detail |
|----------|--------|
| Persistence | Timer state is saved in localStorage, survives page navigation, tab switches, and browser refresh |
| Scope | Keyed per site -- each site has its own independent timer |
| Concurrent timers | Up to 3 timers can run simultaneously across different clients |
| Time increments | Logged in 15-minute increments (rounded to nearest 15 min on stop) |
| Auto-stop cap | Timer automatically stops at **8 hours** to prevent forgotten timers |
| Cap warning | In the last 60 minutes before auto-stop, the hint switches to an orange countdown |
| Crash protection | Stopping the timer keeps the elapsed time in localStorage until the work entry is saved. Refreshing the page reopens the Log Work modal with the duration pre-filled |

## Timer Controls

| Control | Action |
|---------|--------|
| **Start** | Begins a new timer for the current client |
| **Pause** | Freezes the timer; elapsed time is preserved |
| **Resume** | Resumes from where it was paused |
| **Stop** | Stops the timer and opens the Log Work modal with time pre-filled |
| **Discard** | Cancels the timer after a confirmation prompt |

## Topbar Indicator

When a timer is running, a **purple pill** appears in the topbar header to the left of the username. Each pill shows:

- Pulsing stopwatch icon (dims when paused)
- Live `HH:MM:SS` clock
- Client/site name
- Click to navigate directly to that client's Activity Logs tab

### Multi-Timer Display

- Up to **3 timer pills** displayed simultaneously
- Running timers sort first, then by elapsed time (longest first)
- Paused timers appear dimmed
- If more than 3 timers are active, only the top 3 show (running ones prioritized)

### Suppression

The topbar timer pills automatically hide when you're on the Activity Logs tab for a client (since the full timer UI is visible there). They reappear when you navigate to any other tab or page.

## localStorage State

Timer state is stored per site with the key `almaseo_work_timer_{siteId}`. The state object contains:

| Field | Purpose |
|-------|---------|
| `startTs` | Timestamp when the timer started (or resumed) |
| `pausedElapsed` | Accumulated milliseconds from previous running segments |
| `running` | Whether the timer is currently running |
| `stopped` | Whether the timer was stopped but the entry not yet saved |
| `siteName` | Client name (for topbar display) |
| `siteId` | Site ID (for topbar navigation link) |
| `stoppedHours` | Pre-calculated hours for modal pre-fill (set on stop) |
| `stoppedMinsRounded` | Pre-calculated rounded minutes for modal pre-fill (set on stop) |

## Notes / Edge Cases

- Starting a timer on a site that already has one running replaces the existing timer.
- The topbar indicator uses a global `window.TopbarTimer` API with `refresh()` and `suppress()` methods. Activity Logs calls `suppress(true)` on init and the tab switcher calls `suppress(false)` when leaving.
- Client name is backfilled for timers started before the siteName field was added -- the next time you visit that client's Activity Logs tab, the name is written to the existing state.
