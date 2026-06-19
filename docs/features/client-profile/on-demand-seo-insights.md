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

---

## Live SERP Check

**Location:** Client Profile > Website Analysis > Live SERP Check tab

Live SERP Check lets users query Google's live search results for any keyword and see a structured breakdown of what Google is actually showing — not just the blue links, but the full SERP landscape.

The tab contains two tools, both powered by the same data credit system as the SEO Snapshot Card.

### SERP Feature Scanner

Enter up to 10 keywords and see, for each one:

| Data Point | What It Shows |
|-----------|---------------|
| AI Overview | Whether Google shows an AI-generated answer, including the full overview text and cited sources |
| Featured Snippet | Whether a Featured Snippet exists, who holds it, and what it says |
| People Also Ask | All PAA questions Google surfaces for this keyword |
| Top Organic Results | The top 5 organic results with titles, URLs, and positions |
| Site Presence | Whether your client's site appears in organic results, AI Overview sources, or the Featured Snippet |

**Site-aware results:** The client's domain is automatically checked against all results. When the site appears, it's highlighted with a green "Your site" badge. When it doesn't appear, a warning flags specific threats:

- "Google is answering this with AI — users may not click through"
- "A competitor holds the Featured Snippet"

**Credit cost:** 25 data credits per keyword

**Cache:** Results are cached for 6 hours. Viewing cached results costs 0 credits.

### Keyword Volume & Competition

Enter up to 20 keywords and get Google Ads data for each:

| Metric | Description |
|--------|-------------|
| Monthly Search Volume | Average monthly searches |
| CPC | Cost-per-click (USD) |
| Competition | Google Ads competition level (0-100) |
| Difficulty | Keyword difficulty score (0-100) |

Results are sorted by volume descending and color-coded by competition/difficulty level (Low/Medium/High).

**Credit cost:** 25 data credits per keyword

**Cache:** Results are cached for 24 hours. Viewing cached results costs 0 credits.

### Confirmation Flow

Both tools follow the same confirmation pattern:

1. User enters keywords in the text area
2. A live cost hint updates as they type (e.g. "3 keywords = 75 credits")
3. User clicks the action button
4. A confirmation modal appears showing:
    - Credit cost of this action
    - Current credit balance
    - Projected balance after the transaction
5. If the user has insufficient credits, the modal shows a link to the Data Credits page to purchase more
6. User confirms — the API call fires and results display
7. The balance bar at the top of the tab refreshes automatically

### Credit Balance Bar

A persistent balance bar at the top of the Live SERP Check tab shows:

- Total available data credits
- Monthly remaining vs. extra credit breakdown
- "Get More Credits" link to `/data-credits`

The balance loads automatically when the tab opens and refreshes after every action.

### Why Live SERP Check Matters

- **Spot AI Overview threats** — If Google is answering a query with AI, users may never click through to the client's site. Know which keywords are affected before investing in content.
- **Find Featured Snippet opportunities** — See which keywords have snippets and who holds them. If it's a weak competitor, the client can take it with targeted content.
- **Discover content ideas** — The People Also Ask questions Google shows are exactly what the audience wants answered. Use them for blog posts, FAQ pages, and service pages.
- **Check keyword viability** — Before writing content, see the real search volume, CPC, and competition level so you know the keyword is worth targeting.
- **Track changes over time** — Results are saved. Come back later and refresh to see if Google has changed how it answers key queries.

---

## Requirements

- **External provider:** Configured via server environment variable (admin setup)
- **Stripe:** Required for credit pack purchases (optional — monthly included credits work without Stripe)
- **No AI required:** This feature does not use AI models. Powered by external SEO data APIs.

## Why It Matters

Gives agencies instant access to competitive SEO metrics and live SERP intelligence for any client site without leaving AlmaSEO. Cached snapshots make repeated views free, and the credit system ensures costs are transparent and predictable. Agencies can quickly assess a client's organic visibility, investigate keyword opportunities, spot AI Overview threats, and track changes over time — all from the same profile page where they manage content, automation, and reporting.
