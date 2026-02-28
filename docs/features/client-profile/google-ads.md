# Google Ads

**Tier:** Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    Unlike Analytics (read-only) and Search Console (SEO backbone), Google Ads is an active control surface: it can create and modify real campaigns, keywords, and responsive search ads. That makes it a strong agency feature and a potential “growth lever” demo, while GAQL-backed reporting and Keyword Planner create a bridge from paid keyword signals to content strategy.

## Overview

Connection & setup:
- OAuth connect / disconnect (one-click).
- Customer ID configuration (saved per client).
- Refresh Data button to reload all Ads data across the tab.
- Connection diagnostics endpoint that verifies developer token, OAuth token, Customer ID, and client creation status.

Sub-tabs:
1) Campaign Management (lightweight, not full Ads editor)
- Campaigns: list campaigns with status, budget, bid strategy. Create campaigns (Search type) with name, budget, bid strategy via Google Ads API. Enable/Pause campaigns.
- Keywords: list keywords with status, match type, bid. Add keywords by selecting an existing ad group (grouped by campaign), entering keywords (one per line), choosing match type (Broad/Phrase/Exact), and setting a default bid.
- Ads: list ads with status and ad group. Create Responsive Search Ads in existing ad groups by providing up to 3 headlines (30 chars), 2 descriptions (90 chars), display URL, and final URL.
- Budget & bidding: daily + monthly budget inputs, bid strategy selector (Maximize Clicks, Maximize Conversions, Target CPA, Manual CPC), default bid setting.

2) Analytics & Reports
- Overview metrics (last 30 days + % change vs prior 30): Impressions, Clicks, CTR, Cost.
- Date controls: 7d / 30d / 90d / 1y presets + custom range picker.
- Charts: performance trends (daily impressions + clicks), cost distribution doughnut (spend by campaign type).
- Tables: campaign performance; top keywords (incl. quality score); ad performance; geographic breakdown; device breakdown.
- Quality score insights cards: average quality score, high/low quality keyword counts, improvement opportunities.

3) Keyword Planner
- Seed keyword input and URL-based topic extraction.
- Location targeting.
- Results table with volume, competition level/index, CPC range (low/high), plus filtering and sorting.
- Historical monthly trends (last 12 months) for selected keywords.
- Fallback behavior: falls back to SerpAPI when Google Ads is not connected. If connected but a Google Ads API call fails (for example, permission denied), it returns an error and does not fall back.

Not supported (current scope):
- Create ad groups (ad groups must already exist).
- Delete campaigns, keywords, or ads.
- Edit existing ads or keywords.
- Advanced bid adjustments, audience targeting, ad extensions.
- Bulk operations or automated rules.

## Why It Matters

Lets teams manage and analyze paid search directly inside AlmaSEO, and compare paid performance (spend, conversions, top keywords) alongside organic search and site analytics for a single client.

## Requirements

- **Integrations:** Google API

## Access Control

**Permission Mode:** Configurable per client

## Target Audience

Agencies, Freelancers

