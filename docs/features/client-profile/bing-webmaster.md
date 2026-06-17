---
title: "Bing Webmaster Tools"
slug: "bing-webmaster"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "CP-BING-WMT"
last_updated: "2026-06-17"
---

# Bing Webmaster Tools

**Tier:** Core/Free | **Type:** Integration + User-Facing UI

!!! tip "Key Insight"
    Bing powers Microsoft Copilot search results and holds meaningful traffic share in certain verticals (legal, finance, enterprise). This integration surfaces Bing-specific search data that Google-only reporting completely misses — including queries, crawl health, keywords, and link data from Microsoft's index.

## Overview

The Bing Webmaster Tools integration connects each customer's Bing account to AlmaSEO via a per-customer API key. It provides a 9-tab dashboard with Bing-branded visual identity (blue-purple gradient palette, Segoe UI typography) that is visually distinct from the Google Search Console panel.

**Tabs and what they show:**

| Tab | What It Shows |
|-----|---------------|
| **Overview** | KPI cards (clicks, impressions, CTR, avg position) + top search queries + top pages |
| **Crawl Stats** | Pages indexed, pages crawled, crawl errors, inbound links, crawl settings, recently fetched URLs |
| **Crawl Issues** | URLs with HTTP errors (301s, 404s, 500s) sorted by inbound link impact + blocked URLs |
| **URL Tools** | URL Inspector (index status, discovery date, document size, anchors) + URL Directory Explorer (child pages under a parent) |
| **Keywords** | Related Keywords Finder (enter a keyword, get Bing's related terms) + Query Traffic Over Time (daily trend for a query) |
| **Query Analysis** | Pages Ranking for a Query (which pages rank for a specific query) + Queries by Page (which queries drive traffic to a specific page) |
| **Links** | Inbound link counts, pages with links table, Inbound Links for a URL drill-down, connected pages count |
| **Sitemaps** | Daily/monthly URL submission quotas, submitted sitemaps table with processing status, per-sitemap details |
| **Site Config** | Country/region targeting, site roles & access, site migration history, URL query parameters, page preview blocks, deep link blocks |

## How to Connect

1. **Create or sign in** to [Bing Webmaster Tools](https://www.bing.com/webmasters/).
2. **Add your site** and verify ownership using one of Bing's methods (DNS record, meta tag, or CNAME). Bing can only return data for verified sites.
3. **Copy your API key** from [Settings > API Access](https://www.bing.com/webmasters/apikey). One key works for all sites in your Bing account.
4. **Paste the key** in AlmaSEO: go to your site's Client Profile, click **Bing Webmaster** in the sidebar, and paste the key in the connect form.

AlmaSEO validates the key by calling Bing's `GetUserSites` endpoint and confirms your site URL appears as verified. If the site isn't verified, connection is blocked with a clear error message.

!!! warning "Site must be verified"
    Bing's API returns `NotAuthorized` for unverified sites. If you see this error, complete the verification process in Bing Webmaster Tools first. The site must show `IsVerified: true` in your Bing account.

## Credential Storage

- API keys are **Fernet-encrypted** and stored in the same `google_oauth_tokens` table used for Google services, with `service_type = 'bing_webmaster'`.
- Keys are per-user, per-site, and decrypted only at request time.
- No OAuth flow — Bing uses static API keys that don't expire.
- Users can disconnect and reconnect at any time.

## API Coverage

The integration implements **all 34 read-only tools** from the Bing Webmaster API:

**Search Performance (4 tools)**

- `GetUserSites` — validate API key, list verified sites
- `GetRankAndTrafficStats` — daily clicks/impressions
- `GetQueryStats` — top queries with clicks, impressions, CTR, position
- `GetPageStats` — top pages by search performance

**Crawl Health (6 tools)**

- `GetCrawlStats` — daily crawl volume, indexed pages, errors, status codes
- `GetCrawlIssues` — URLs with HTTP errors
- `GetCrawlSettings` — current crawl rate configuration
- `GetUrlInfo` — index status for a specific URL
- `GetFetchedUrls` — URLs Bing has fetched
- `GetFetchedUrlDetails` — detailed fetch info per URL

**Keywords (6 tools)**

- `GetKeyword` — performance for a single keyword
- `GetKeywordStats` — historical keyword trends by country/language
- `GetRelatedKeywords` — related search terms
- `GetQueryPageStats` — which pages rank for a query
- `GetPageQueryStats` — which queries drive traffic to a page
- `GetQueryTrafficStats` — click/impression trend over time

**Links (3 tools)**

- `GetLinkCounts` — inbound link summary
- `GetUrlLinks` — inbound links to a specific URL
- `GetConnectedPages` — pages linking to the site

**Sitemaps & Feeds (4 tools)**

- `GetFeeds` — submitted sitemaps and processing status
- `GetFeedDetails` — detailed info per sitemap
- `GetUrlSubmissionQuota` — daily/monthly submission limits
- `GetContentSubmissionQuota` — content submission limits

**Site Configuration (8 tools)**

- `GetBlockedUrls` — URLs blocked from crawling
- `GetDeepLinkBlocks` — deep link blocks
- `GetQueryParameters` — URL normalization parameters
- `GetCountryRegionSettings` — geo-targeting configuration
- `GetActivePagePreviewBlocks` — rich snippet blocks
- `GetSiteMoves` — site migration history
- `GetSiteRoles` — users with access
- `GetChildrenUrlInfo` — child URLs under a parent

**Excluded (write/destructive tools):** `AddSite`, `RemoveSite`, `SubmitUrl`, `SubmitContent`, `SubmitSitemap`, `RemoveFeed`, `AddBlockedUrl`, and all other `Add*/Remove*/Submit*/Update*` endpoints are intentionally not implemented.

## Cost & Tracking

- **Bing's API is free** — no per-call charges.
- All API calls are logged to the `usage_events` table with `vendor = 'bing'` and `cost_cents = 0` for volume visibility and abuse detection.
- Bing calls appear in the admin cost dashboard alongside OpenAI, SerpAPI, and DataForSEO usage.

## Bing API Key Scope

The Bing API key is **account-scoped, not site-scoped**. One key grants access to all sites verified under that Bing Webmaster account. AlmaSEO mitigates this by:

1. Validating on connect that the specific AlmaSEO site URL is verified in Bing.
2. Passing the specific `siteUrl` parameter on every API call so Bing only returns data for that site.
3. Never enumerating or exposing other sites the key has access to.

## Data Handling

- All data is **fetched live** from the Bing API on each tab visit. No data is cached or stored in the AlmaSEO database.
- Each tab **lazy-loads** — API calls only fire when the user clicks into that tab, keeping the Overview tab fast.
- Bing returns per-query per-date rows — the client aggregates these across dates before displaying.
- Bing's OData date format (`/Date(epoch)/`) is automatically parsed to `YYYY-MM-DD`.

## Requirements

- **Integration:** Bing Webmaster Tools API (`ssl.bing.com/webmaster/api.svc/json`)
- **Credential:** Per-customer Bing API key (obtained from Bing Webmaster Tools settings)
- **Site verification:** Site must be added and verified in Bing Webmaster Tools
- **No AI dependency:** This feature does not use any AI models

## Comparison with Google Search Console

| Aspect | Google Search Console | Bing Webmaster Tools |
|--------|----------------------|---------------------|
| Auth method | OAuth 2.0 (redirect flow) | Static API key (paste in dashboard) |
| Token refresh | Automatic via refresh_token | Not needed (keys don't expire) |
| Data window | Up to 16 months | Varies by endpoint (typically 6 months) |
| API cost | Free | Free |
| UI identity | Standard AlmaSEO card styling | Bing-branded gradient palette |
| Inner navigation | Sections within one scroll | 9 separate pill tabs |

## Target Audience

Agencies, DIY Business Owners, Freelancers — anyone who wants visibility into Bing/Copilot search performance alongside their Google data.
