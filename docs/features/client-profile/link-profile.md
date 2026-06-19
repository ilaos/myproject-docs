# Link Profile

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Real backlink data powered by SE Ranking's Backlinks API — not snippet guessing. One click gives you domain authority, top referring domains ranked by authority, anchor text distribution, new/lost links, and a competitor gap analysis. All cached as snapshots (24h). Uses data credits (150/refresh, 100/competitor gap).

## Overview

Link Profile is a backlink intelligence panel on the Client Profile that shows who links to a site, how strong those links are, and what's changed recently. It replaces the former NAP Shield feature with real crawled backlink data.

### What It Shows

| Panel | Data |
|-------|------|
| **Profile Summary** | Domain Authority (InLink Rank), total backlinks, referring domains, dofollow %, edu/gov link counts |
| **Top Referring Domains** | Top 50 domains linking to the site, sorted by authority score. Shows backlink count, dofollow ratio bar, and first-seen date |
| **Anchor Text Distribution** | Top 30 anchor texts by backlink count, with referring domain count and dofollow count |
| **New & Lost Links** | Referring domains gained and lost in the past 30 days, split into two columns with authority badges |
| **Competitor Link Gap** | Enter a competitor domain to see high-authority domains linking to them but not to you. Separate credit charge (100 credits) |

### How It Works

1. User clicks **Create Snapshot** (or **Refresh** if a snapshot exists)
2. Confirmation modal shows credit cost (150), current balance, and projected balance
3. Backend makes 4 SE Ranking API calls bundled under one charge:
    - `/backlinks/summary` — totals and authority
    - `/backlinks/refdomains` — top 100 referring domains by authority
    - `/backlinks/anchors` — top 100 anchor texts
    - `/backlinks/new-lost-refdomains` — gained/lost in last 30 days (optional, plan-dependent)
4. Results are normalized and saved as a snapshot in `seranking_snapshots` (24h cache)
5. Cached snapshots load for free on subsequent visits — no additional API calls or credits

### Link Alerts

When a profile is refreshed, the new/lost data is automatically analyzed for significant events:

- **High-authority link gained** (DA 50+) — success notification
- **High-authority link lost** (DA 50+) — warning notification
- **Bulk link loss** (5+ domains in 30 days) — warning notification
- **Link velocity** — net gained/lost summary

Significant alerts are persisted as notifications (visible in the notification bell). Alert generation costs zero additional credits — it uses data already fetched during the refresh.

## Why It Matters

- **Backlinks are the #1 ranking factor** that most small business owners have zero visibility into
- **Real data, not guesswork** — powered by SE Ranking's backlink crawler, not Google snippet parsing
- **Competitor intelligence** — the gap analysis shows exactly where to focus outreach efforts
- **Authority context** — knowing your DA and who links to you is essential for any SEO conversation

## Requirements

- **Integrations:** SE Ranking API (`SERANKING_API_KEY` environment variable)
- **Data Credits:** 150 per profile refresh, 100 per competitor gap analysis
- **Depends On:** Client Profile (site must exist), Data Credits system

## Access Control

**Permission Mode:** Login required, site ownership verified

## Target Audience

Agencies, DIY Business Owners, Freelancers

## Technical Details

### Files

| File | Purpose |
|------|---------|
| `routes/link_profile_routes.py` | Blueprint with 4 endpoints: data, refresh, balance, gap |
| `templates/client_profile/link_profile.html` | Full template with Jinja rendering + JS |
| `integrations/seranking_client.py` | `get_link_profile()` and `get_link_gap()` bundle functions |
| `integrations/seranking_credit_guard.py` | ACTION_REGISTRY entries for `seranking.link_profile` and `seranking.link_gap` |

### API Endpoints

| Endpoint | Method | Credits | Purpose |
|----------|--------|---------|---------|
| `/api/site/<id>/link-profile/data` | GET | 0 | Return cached snapshot |
| `/api/site/<id>/link-profile/refresh` | POST | 150 | Fetch fresh data from SE Ranking |
| `/api/site/<id>/link-profile/balance` | GET | 0 | Credit balance for cost preview |
| `/api/site/<id>/link-profile/gap` | POST | 100 | Competitor backlink gap analysis |

### Database

- Snapshots stored in `seranking_snapshots` table with `data_type='link_profile'`
- Credit usage logged to `usage_events` (vendor=seranking)
- Link alerts persisted to `notifications` table

## Notes / Edge Cases

- The `/backlinks/new-lost-refdomains` endpoint may not be available on all SE Ranking API plans. If unavailable, the profile loads with 3 panels instead of 4 — the New & Lost section shows empty gracefully.
- Competitor gap analysis compares the top 200 referring domains by authority for each side. Very large sites may have gaps beyond this window.
- Cached snapshots expire after 24 hours. Viewing a cached snapshot costs zero credits.
- The feature replaced NAP Shield in the sidebar. NAP Shield routes still exist in `dashboard.py` but are unreferenced from the UI.
