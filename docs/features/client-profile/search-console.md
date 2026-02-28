# Search Console

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    GSC is the most heavily integrated Google service in AlmaSEO and the core data backbone for content strategy. It directly powers Content Gaps, SEO Recovery 911, keyword seeding for content generation, Search Appearance-driven schema recommendations, and URL-level diagnostics.

## Overview

What it shows:
1) Connection Status: connected property URL + property type badge, change/disconnect controls.
2) Performance KPIs (6): Total Clicks, Impressions, Avg CTR, Avg Position, Total Queries, Indexed Pages (with trends).
3) Performance Charts: time-series trends + traffic distribution (pie chart).
4) Top Content: top performing pages + top queries by clicks/impressions.
5) Geographic & Device: country breakdown + desktop/mobile/tablet split.
6) Technical Health: sitemap status, indexing stats, coverage issues (errors/warnings/valid).
7) Content Gaps Analysis: AI-scored opportunities (No Page, Low CTR, Poor Ranking, No Clicks) with ability to generate articles from gaps.
8) Search Appearance: SERP feature analysis (rich results, featured snippets, AMP, etc.) with improvement recommendations.
9) URL Inspector: per-URL diagnosis (index coverage, canonicals, mobile usability, rich results validation).

Features that depend on GSC:
- Content Gap Analysis: identifies keyword opportunities from GSC queries (impressions, CTR, position).
- SEO Recovery 911: uses GSC metrics (clicks, impressions, dead-zone keywords) to build audit reports + recovery plans.
- Blog Generator: pre-populates target keywords/context from gaps; supports indexing submission workflows.
- AI Content Recommendations: clusters queries by intent, finds patterns and seasonality.
- Schema Generator: uses Search Appearance data to suggest schema for rich results.

OAuth / connection flow:
- Connect → /google/search-console/connect → Google OAuth consent.
- Redirect to property selection (user must pick a property).
- Property saved to http://sites.google_search_console_property.
- Tokens encrypted (Fernet) stored in google_oauth_tokens; auto-refresh on expiry; reconnect if refresh fails.

Key technical notes:
- 16-month (486-day) max window enforced in date pickers (GSC API limit).
- Production template: google_search_console_simplified.html (~3,150 lines). Other templates exist but are not used.
- ~20+ backend endpoints across performance, technical health, gaps, search appearance, and URL inspection.

## Why It Matters

Gives a complete view of search performance and indexing health, and turns GSC data into actionable content opportunities (including generating content directly from gaps).

## Requirements

- **Integrations:** Google API

## Target Audience

Agencies, DIY Business Owners, Freelancers

