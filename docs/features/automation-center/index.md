---
title: "Automation Center"
slug: "automation-center"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: "PL-AUTOMATION-CENTER"
last_updated: "2026-03-04"
---

# Automation Center

## Overview

Automation Center is the fleet-wide operations dashboard at `/automation`. It provides a single view of automation health, queue status, job history, and system controls across **all sites** — not just one.

This is distinct from the per-site **Content Automation** settings inside each Client Profile. Client Profile handles one site's automation configuration (topics, schedule, frequency). Automation Center is the control room that monitors everything at once — queue depth, worker status, failure rates, dead letter queue, and system mode — with admin-only controls for pausing, resuming, and managing the queue.

**Hierarchy:**
- `/automation` — Fleet-wide dashboard (this feature)
- `/site/<id>/profile → Automations tab` — Per-site automation settings

---

## What It Does

### System Status

The top of the dashboard shows the current state of the automation system at a glance:

| Indicator | What It Shows |
|-----------|--------------|
| **Mode** | Current system mode — LIVE (active), DRY-RUN (running but not publishing), SHADOW (monitoring only), CANARY (gradual rollout), OFF, or OFFLINE |
| **Leader** | Hostname of the active automation worker |
| **Queue** | Current queue depth and in-progress job count |
| **DLQ** | Dead letter queue depth (red warning if > 0) |
| **Cap** | Daily publication cap status |

Below the status row:

| Tile | What It Shows |
|------|--------------|
| **Next Run Windows** | The 3 daily publication slots (8am, 2pm, 8pm ET) with next occurrence in UTC |
| **WordPress Backfill** | Status and pending/processed counts for WordPress content backfill |
| **WordPress Upsert** | Status and 24-hour update count for WordPress content sync |
| **Post Verification** | Pass/fail counts for post verification checks (24h) |
| **IndexNow** | Submitted/failed counts for search engine submissions (24h) |

### Automation Insights KPIs

Five primary KPIs displayed as real-time counters:

| KPI | What It Measures |
|-----|-----------------|
| **Posts (24h)** | Total posts created across all sites in the last 24 hours |
| **Verify (24h)** | Post verification success/failure ratio |
| **IndexNow (24h)** | Search engine submission success/failure ratio |
| **Queue** | Current queue depth (jobs waiting to run) |
| **DLQ** | Current dead letter queue depth (jobs that failed permanently) |

### Recent Jobs

A searchable, filterable table of all automation jobs across all sites.

**Columns:** Job ID, Site, Status, Topic, Created, Started, Finished, Actions

**Filters:**
- By status: All, Queued, Running, Finished, Failed
- By site: All sites or a specific site
- By search term (URL, site name, topic)

**Features:**
- Auto-refreshes every 10 seconds
- Paginated (up to 100 per page)
- Export to CSV
- Color-coded status badges: green (finished), red (failed), blue (running), amber (queued)

### Dead Letter Queue (DLQ)

Jobs that have **failed permanently** — exceeded retry attempts or hit catastrophic errors — are moved to the dead letter queue. The DLQ prevents failed jobs from clogging the main queue while retaining them for manual inspection.

**What the DLQ panel shows:**
- Job ID, site, topic, creation date, number of attempts, error message
- Site filter and pagination
- Export to CSV

**Admin actions on DLQ items:**
- **Retry** — moves the job back to "queued" with attempts reset to 0
- **Delete** — permanently removes the job

### Per-Site Automation Cards

A grid of cards showing every site with automation configured. Each card displays:

- Site name and enabled/disabled status
- Automation frequency (daily, weekly, biweekly, monthly)
- Last run timestamp and next scheduled run
- Queue depth for that site
- Color-coded status (idle, queued, running, finished, failed)
- **Run Now** button (admin-only) to trigger an immediate manual run

Clicking a site card navigates to that site's Client Profile → Automations tab for per-site configuration.

### Queue Management (Admin-Only)

Four queue control actions available to administrators:

| Action | What It Does |
|--------|-------------|
| **Pause** | Stops all job processing without clearing the queue. Sets the `global_enable` flag to false. |
| **Resume** | Restarts job processing from where it was paused. |
| **Retry All Failed** | Moves all failed jobs back to "queued" with attempts reset to 0. |
| **Clear Pending** | Permanently deletes all queued jobs. Destructive — cannot be undone. |

All admin actions are logged with the actor's email for audit trail.

---

## Why It Matters

- **Fleet-wide visibility** — instead of checking automation status site by site, see every site's queue health, job status, and failure rates on one page.
- **Catch failures early** — the DLQ and failure rate indicators surface problems before they compound. A spike in failed jobs across multiple sites often indicates an upstream issue (API rate limits, OpenAI outages, WordPress connectivity) that needs attention.
- **Admin controls prevent cascading problems** — pausing the queue during an API outage stops failed jobs from piling up. Retrying after the issue resolves is one click.
- **Capacity planning** — queue depth, daily caps, and publication rate KPIs show whether the system is keeping up with the configured publishing schedules across all sites.
- **Accountability** — every admin action (pause, resume, retry, delete) is logged with the actor's identity and timestamp.

---

## How to Use It

### Monitoring Day-to-Day Operations

1. Navigate to **Automation Center** (`/automation`) from the sidebar.
2. Check the **System Status** row — confirm the mode is LIVE and the leader worker is active.
3. Review the **KPI tiles** — Posts (24h) shows production volume; DLQ > 0 means failures need attention.
4. Scan the **Per-Site Cards** — look for sites with failed or stuck jobs (red status).

### Investigating Failures

1. Check the **Recent Jobs** panel — filter by status "Failed" to see all failures.
2. Click into a failed job to see the error message and attempt count.
3. If the failure is transient (API timeout, rate limit), use **Retry All Failed** to re-queue.
4. If the failure is permanent (bad configuration, invalid topic), check the **DLQ** panel.
5. In the DLQ, decide per-job: **Retry** (if the root cause is fixed) or **Delete** (if the job should be discarded).

### Responding to System Issues

| Scenario | Action |
|----------|--------|
| OpenAI API outage | **Pause** the queue → wait for resolution → **Resume** |
| High failure rate spike | Check error messages for pattern → fix root cause → **Retry All Failed** |
| DLQ building up | Review each item → fix site-level configuration → **Retry** or **Delete** |
| Queue growing faster than processing | Check worker health → verify leader is active → check daily caps |
| Need to stop all automation | **Pause** the queue (preserves all jobs for later) |

### Triggering Manual Runs

1. Find the target site's card in the Per-Site grid.
2. Click **Run Now** (admin-only).
3. The system inserts a job with an idempotency key — duplicate rapid clicks are prevented (one run per site per minute).

---

## Key Settings / Options

### System Modes

| Mode | Behavior | Badge Color |
|------|----------|-------------|
| LIVE | Active, processing and publishing jobs normally | Green |
| DRY-RUN | Running pipeline but not publishing to WordPress | Amber |
| SHADOW | Monitoring only, no job execution | Blue |
| CANARY | Gradual rollout — processing a subset of sites | Blue |
| OFF | Automation disabled globally | Gray |
| OFFLINE | Worker unreachable, operations halted | Gray |

### Guardrails & Safety

| Guardrail | What It Prevents |
|-----------|-----------------|
| **Daily caps** | Per-site configurable limit (1-10 posts/day, default 1). Prevents over-publishing. |
| **Circuit breaker** | Trips automatically if failure rate exceeds 20% across last 20+ jobs, or if p95 job duration exceeds 120 seconds. Disables processing until manually reset. |
| **Idempotency keys** | Prevents duplicate manual runs — one run per site per action type per minute. |
| **Rate limiting** | 3-second minimum between admin actions per user. |
| **Duplicate prevention** | Same job cannot be re-enqueued while already in queue. |
| **Topic guards** | Per-site topic whitelist/blacklist prevents forbidden topics from being automated. |

### Access Control

| Capability | Admin | Non-Admin |
|-----------|-------|-----------|
| View dashboard, KPIs, status | Yes | Yes |
| View recent jobs and DLQ | Yes | Yes (read-only) |
| Pause / Resume queue | Yes | No |
| Retry All Failed | Yes | No |
| Clear Pending | Yes | No |
| Retry / Delete DLQ items | Yes | No |
| Run Now (per-site) | Yes | No |
| Edit runtime flags | Yes | No |

### Publication Schedule

The automation worker runs on a fixed daily schedule with 3 publication windows:

| Window | Time (ET) |
|--------|-----------|
| Morning | 8:00 AM |
| Afternoon | 2:00 PM |
| Evening | 8:00 PM |

Per-site frequency settings (daily, weekly, biweekly, monthly) determine which windows a site participates in.

---

## Notes / Edge Cases

- **Worker lock** — only one automation worker runs at a time, enforced by a database lock (`automation_locks` table) with heartbeat monitoring. If the heartbeat is older than 5 minutes, the worker is considered dead.
- **Circuit breaker auto-trips** — if the failure rate exceeds 20% or p95 duration exceeds 120 seconds, the circuit breaker trips automatically. This protects against cascading failures but means automation will stop until an admin investigates and resets.
- **DLQ is not automatic cleanup** — jobs in the dead letter queue stay there indefinitely until an admin manually retries or deletes them. They don't auto-expire.
- **Clear Pending is destructive** — unlike Pause (which preserves jobs), Clear Pending permanently deletes all queued jobs. There is no undo.
- **All admin actions are logged** — pause, resume, retry, delete, and manual run actions include the actor's email in the log for accountability.
- **Per-site automation is configured separately** — Automation Center is for monitoring and fleet-level controls. To change a site's frequency, daily cap, topics, or schedule, go to that site's Client Profile → Automations tab.
