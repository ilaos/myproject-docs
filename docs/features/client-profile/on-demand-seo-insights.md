# On-Demand SEO Insights

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Most of AlmaSEO works without data credits. On-Demand SEO Insights gives users access to fresh competitive SEO data when they want it — cached snapshots are free, live refreshes use data credits. This is the first feature in the platform that connects to paid external SEO data providers, and it establishes the pattern for all future external data features.

## Overview

On-Demand SEO Insights provides competitive SEO data for any client site directly on the profile Overview tab. Users can see organic keyword counts, traffic estimates, traffic value, ranking distribution, and paid search metrics without leaving the client profile.

Data is stored as **snapshots** — cached results that are free to view as many times as needed. When a user wants the latest data, they can request a **live refresh**, which pulls fresh data from an external SEO data provider and costs 250 AlmaSEO data credits.

### SEO Snapshot Card

The snapshot card appears on the client site profile Overview tab (between Profile Completeness and Quick Stats) and shows:

**When a saved snapshot exists:**

- Organic Keywords count
- Organic Traffic estimate
- Traffic Value (USD)
- Top 1-5 Rankings count
- Paid Keywords, Paid Traffic, Paid Cost (if the domain has paid search activity)
- Snapshot date with "No credits used" badge
- "Refresh live data" button

**When no snapshot exists:**

- "No saved SEO snapshot yet" message
- "Create live snapshot" button with credit cost displayed

### Live Refresh Confirmation

Live refreshes require explicit confirmation before any external API call is made:

1. User clicks "Refresh live data" or "Create live snapshot"
2. A confirmation prompt appears showing the data credit cost
3. No external call happens until the user confirms
4. After confirmation, exactly one provider call is made
5. The result is saved as a new snapshot

### What the Snapshot Includes

Each snapshot contains organic and paid search data for one domain in one regional database:

| Metric | Description |
|--------|-------------|
| Organic Keywords | Total keywords the domain ranks for |
| Organic Traffic | Estimated monthly organic visits |
| Traffic Value (USD) | Estimated cost to buy equivalent traffic via ads |
| Top 1-5 | Keywords ranking in positions 1-5 |
| Top 6-10 | Keywords ranking in positions 6-10 |
| Top 11-20 | Keywords ranking in positions 11-20 |
| New Keywords | Keywords gained since last data update |
| Lost Keywords | Keywords lost since last data update |
| Paid Keywords | Active paid search keywords (if any) |
| Paid Traffic | Estimated paid search visits (if any) |
| Paid Cost (USD) | Estimated paid search spend (if any) |

### Caching

- Snapshots are cached for **24 hours**
- Viewing a cached snapshot costs **0 credits**
- Cache keys include: domain + regional database + data type
- Multiple regions for the same domain are cached independently

### Credit Cost

- **Cached/saved snapshot:** 0 credits
- **Live refresh:** 250 AlmaSEO data credits per domain per region

### Regional Database

Currently defaults to US database. Future versions may allow region selection per client site.

## Data Credits

On-Demand SEO Insights introduces the **AlmaSEO Data Credit** system. Data credits are the internal currency for requesting fresh data from paid external providers.

### Monthly Included Credits

Paid plan subscribers receive monthly included data credits that reset each billing period:

| Plan | Monthly Included Credits |
|------|--------------------------|
| Early Access | 25,000 |
| Pro | 25,000 |
| Private Tester | 5,000 |
| Free Trial | 0 |

### Extra Data Credits

Users can add extra data credits from the **Data Credits** page (accessible from the sidebar). Extra credits persist until used and are separate from monthly included credits.

Available credit packs:

| Pack | Credits | Price |
|------|---------|-------|
| Small | 25,000 | $10 |
| Standard | 100,000 | $29 |
| Agency | 500,000 | $99 |

### Credit Consumption Order

When a live refresh is performed:

1. Monthly included credits are consumed first
2. Extra data credits are consumed only after included credits are exhausted
3. The exact split is calculated automatically

### Data Credits Page

The `/data-credits` page (linked in the sidebar) shows:

- Monthly included credit allowance
- Credits used this billing period
- Estimated remaining included credits
- Extra data credit balance (if any)
- Total available credits
- Recent usage activity
- Available credit packs (when configured)

### Enforcement Modes

Credit enforcement is configurable (admin setting):

| Mode | Behavior |
|------|----------|
| Off | No warnings or blocks |
| Soft (default) | Warns when credits are low, but allows refresh |
| Hard | Blocks live refresh when total available credits are insufficient |

In all modes:

- Cached/saved data is always free
- Failed or blocked requests never deduct credits

## Requirements

- **External provider:** Configured via server environment variable (admin setup)
- **Stripe:** Required for credit pack purchases (optional — monthly included credits work without Stripe)
- **No AI required:** This feature does not use AI models

## Why It Matters

Gives agencies instant access to competitive SEO metrics for any client site without leaving AlmaSEO. Cached snapshots make repeated views free, and the credit system ensures costs are transparent and predictable. Agencies can quickly assess a client's organic visibility, benchmark against competitors, and track changes over time — all from the same profile page where they manage content, automation, and reporting.
