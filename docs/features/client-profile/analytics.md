# Analytics

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Analytics is intentionally a self-contained reporting window. AlmaSEO’s SEO engine does not consume GA4 data (content gaps, recommendations, SEO recovery, and blog generation use Search Console). This tab exists to give users quick visibility into traffic, engagement, and channel mix, plus a flexible custom query builder.

## Overview

What it shows:
- Overview (default): last-30-day metrics (Users, Sessions, Engagement Rate, Avg Duration), traffic channels breakdown, device split, geographic performance (countries/regions/cities/languages), content performance (landing/exit pages, content depth, SEO insights), temporal analytics (peak hours + hourly distribution), top pages table, and real-time active users widget.
- Acquisition: channel/source/medium analysis with filters.
- Content: landing page + top page engagement.
- Behavior: peak hours, new vs returning.
- Custom Query: GA4 query builder with metrics/dimensions selectors.
- Compare Mode toggle: period-over-period deltas.

Backend endpoints (~16 routes): metrics, traffic sources, top pages, device breakdown, geographic, content performance, temporal, realtime users, metadata for query builder, run query, list properties, save property, current property.

Other features that depend on Analytics:
- None. Analytics is standalone and read-only. It is only referenced by the Client Profile completeness score (connection status), not as an input to the SEO engine.

OAuth / connection flow:
- Connect → /google/analytics/connect → Google OAuth scopes analytics.readonly + analyticsadmin.readonly.
- Property selection (GA4/UA) → saved to ga_properties and google_oauth_http://tokens.ga_property_id.
- Tokens encrypted (Fernet) and auto-refresh on expiry.

Supporting files:
- static/js/ga4_analytics.js (~1,907 lines)
- static/css/ga4_analytics.css (~412 lines)
- utils/ga4_query_http://engine.py (~480 lines)
- Single template (no alternate templates).

## Why It Matters

Provides a clear, in-app view of GA4 traffic and engagement so users can evaluate performance without switching tools.

## Requirements

- **Integrations:** Google API

## Target Audience

Agencies, DIY Business Owners, Freelancers

