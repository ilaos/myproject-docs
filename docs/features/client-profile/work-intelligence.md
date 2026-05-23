---
title: "Work Intelligence"
slug: "work-intelligence"
type: "feature"
status: "complete"
tier: "Pro/Agency"
feature_id: ""
last_updated: "2026-05-23"
---

# Work Intelligence

**Tier:** Pro/Agency | **Type:** User-Facing UI

Part of [Client Retainer Intelligence & Tracking](retainer-tracking.md).

## Overview

An analytics layer that turns raw activity log data into actionable operational intelligence. Surfaces patterns, risks, and insights as slides in the topbar stats ticker carousel, visible from every page. No manual tagging or extra inputs required -- everything is computed from existing logged hours, work types, and retainer settings.

## Where It Appears

All intelligence surfaces in the **topbar stats ticker** -- a rotating carousel at the top of every page. The ticker auto-rotates every 6 seconds with manual arrow navigation. Clicking an arrow stops auto-rotation so you can read a specific slide.

The ticker also shows a slide counter (e.g., "5/18") and an info tooltip explaining how daily targets are calculated.

## Intelligence Modules

### Burnout & Compression Detection

Compares your required daily pace against your actual historical average to detect unsustainable workload compression.

| Slide | Triggers When | Color |
|-------|--------------|-------|
| "Required pace is 2x your average" | Daily target is 2x+ your 30-day average hours/day | Red |
| "Pace 50% above your average" | Daily target is 1.5-2x your average | Orange |
| "Pace 20% above your average" | Daily target is 1.2-1.5x your average | Yellow |
| "X heavy days ahead at Yh/day" | Daily target >= 8h with 3+ workdays left | Orange |

**How it works:** The system calculates your average hours per workday over the last 30 days (only counting days where work was actually logged). It then compares the current required daily pace against this personal baseline, not an arbitrary threshold.

### Momentum Tracking

Compares your progress this month against last month at the same calendar point, and tracks work streaks.

| Slide | Triggers When | Color |
|-------|--------------|-------|
| "+X% ahead of last month at this point" | 10%+ more hours logged by this day vs. same day last month | Green |
| "X% behind last month at this point" | 5-20% fewer hours than last month at the same point | Yellow |
| "X% behind last month at this point" | 20%+ fewer hours than last month | Orange |
| "X-day work streak" | 5+ consecutive workdays with logged hours | Green |
| "X-day work streak building" | 3-4 consecutive workdays with logged hours | Green |

**How it works:** Queries total hours logged from the 1st of the current month through today, and compares against the same date range last month. Streaks count consecutive workdays (respecting the weekend toggle) where any hours were logged.

### Client Silence Detection

Flags clients with active retainers but no recent work logged, helping distinguish operational delays from forgotten accounts.

| Slide | Triggers When | Color |
|-------|--------------|-------|
| "ClientName -- X days since last work" | 21+ days since last logged activity | Red |
| "ClientName -- X days since last work" | 14-20 days since last logged activity | Orange |
| "ClientName -- X days since last work" | 10-13 days since last logged activity | Yellow |

**How it works:** Queries the most recent activity log entry with a duration for each site. Shows up to 2 silent clients, sorted by longest silence first. Clients with no activity history are measured from their billing period start date.

### Time Sink & Scope Creep Detection

Identifies clients consuming disproportionate shares of your total monthly hours and flags potential scope creep.

| Slide | Triggers When | Color |
|-------|--------------|-------|
| "ClientName consumed X% of hours this month" | Any single client accounts for 25%+ of total monthly hours | Purple |
| "ClientName at Xx allocated hours" | A client's logged hours are 2x+ their retainer quota | Orange |

**How it works:** Calculates each client's percentage of total hours logged this month. The scope creep detection compares actual logged hours against the client's retainer_hours quota. Only the worst offender is shown to avoid slide overload.

### Work Category Breakdown

Shows how your time is distributed across different types of work.

| Slide | Triggers When | Color |
|-------|--------------|-------|
| "Time split: Website Work 34% - Meetings 22% - SEO 18%" | At least one work category has 5%+ of monthly hours | Gray |

**How it works:** Groups all activity log entries with duration by their `work_type` metadata field (from the Log Work modal). Shows the top 3 categories by percentage. Work types are mapped to friendly labels:

| Work Type | Display Label |
|-----------|--------------|
| phone_call | Phone Calls |
| client_meeting | Meetings |
| research | Research |
| seo | SEO |
| website_work | Website Work |
| dns_hosting | DNS/Hosting |
| email_correspondence | Email |
| competitor_analysis | Competitor Analysis |
| social_media | Social Media |
| design_work | Design |
| third_party_setup | Third-Party Setup |
| administrative | Admin |
| content_planning | Content Planning |
| google_ads | Google Ads |
| created | Content Creation |
| analyzed | Analysis |

## Existing Ticker Slides

The intelligence slides appear alongside the existing operational slides in the ticker:

| # | Slide | Purpose |
|---|-------|---------|
| 1 | Daily target summary | "Work Xh today to stay on track" |
| 2 | Hours remaining | Total across all sites with days to deadline |
| 3 | Today's progress | Hours logged today vs. target |
| 4 | Urgent tier | Sites due in 1-3 days |
| 5 | Soon tier | Sites due in 4-7 days |
| 6 | On track tier | Sites with 8+ days remaining |
| 7 | Next deadline | Closest billing cycle closing |
| 8 | Cycles closing | Multiple cycles closing within 7 days |
| 9 | Completed sites | Sites with quota fully delivered |
| 10 | Overdelivered | Sites exceeding quota |
| 11 | Zero activity | Sites with 0h logged this period |
| 12 | Heaviest site | Site with the most hours remaining |
| 13 | Almost done | Sites within 2h of completion |
| 14 | Unreachable today | Daily target exceeds available hours today |
| 15+ | Intelligence slides | Compression, momentum, silence, sinks, categories |

## Data Source

All intelligence is computed server-side in the `/api/burnout-check` endpoint. No additional API calls or database tables are needed -- everything uses the existing `activity_log` table, `sites` table (retainer settings), and `users` table (work schedule preferences).

## Notes / Edge Cases

- Intelligence slides only appear when their conditions are met. A healthy, well-paced workload may show very few intelligence slides.
- Momentum comparison requires at least some hours logged last month. If last month has no data, a simpler "Xh logged this month so far" slide appears instead.
- The 30-day historical average only counts days where work was actually done (not zero-hour days), providing a realistic baseline.
- Client silence detection uses `json_extract(metadata, '$.duration_minutes') > 0` to find the last real work entry, ignoring zero-duration system events.
