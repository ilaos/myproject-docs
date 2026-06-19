# SEO Recovery 911

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is a "hard conversation" tool: it turns messy performance drops into an explainable audit, a phased plan with budget expectations, and ready-to-send communication templates. The 17-analysis pipeline goes beyond aggregate metrics to diagnose specific pages, detect SERP changes, validate technical health, and reveal post-click problems — giving agencies a complete pre-click to post-click recovery workflow.

## Overview

### Prerequisites

- **Required:** Google Search Console connected and verified.
- **Recommended:** Link Profile has a snapshot (adds backlink authority context).
- **Optional (enhances audit):** Google Analytics 4 connected (adds post-click diagnostics). Google Ads connected (adds search volume enrichment). DataForSEO credentials configured (adds AI Overview monitoring).

### Audit Configuration (modal)

- Primary focus areas (service keywords).
- Geographic focus (cities/counties).
- Exclude terms (competitors, discontinued services).
- Brand search toggle (include/exclude branded queries).
- Industry selector (Legal, Home Services, Medical, Automotive, Financial, Real Estate, Restaurant, Generic).
- NAP location selector (for multi-location businesses).

### Audit Pipeline

The audit runs 17 analyses across 6 data sources when all integrations are connected. Each phase is non-fatal — if any analysis fails, the rest complete normally.

**Core GSC Analysis (keyword-level, 90-day window):**

1. Fetch raw GSC query data (clicks, impressions, CTR, position).
2. Filter by user config (focus/geo/exclusions/brand).
3. Optional: enrich with search volume when Google Ads is connected.
4. Analyze dead-zone keywords (positions 15-70, high impressions, low clicks).
5. Practice area / service category breakdown (industry-specific with dynamic fallback).
6. Brand vs non-brand traffic split.
7. Issue detection via thresholds (CTR, position, dead-zone count, brand dependency, zero-click keywords, wrong keyword focus).

**Page-Level GSC Intelligence** (`utils/seo_intelligence.py`):

8. **Traffic Drops** — classifies each losing page by root cause: ranking loss (position dropped >2), CTR collapse (position stable but CTR <70% of prior), demand decline (impressions dropped >30%), or disappeared (page no longer in results). Compares current 28 days vs prior 28 days.
9. **Quick Wins** — scores position 4-15 keywords by `impressions × (CTR_at_pos3 - actual_CTR)`. Estimates extra clicks if pushed to position 3.
10. **CTR Opportunities** — finds top-10 pages with CTR below expected benchmark for their position. Identifies title/meta rewrite candidates with estimated click gain.
11. **Content Decay** — identifies pages with monotonic click decline across 3 consecutive 30-day windows (oldest > middle > recent). Flags real content aging, not single-week dips.
12. **Cannibalization** — detects queries served by 2+ pages on the same site, with aggregated impression threshold to filter noise.

**Technical Health** (`utils/seo_technical.py`):

13. **PageSpeed Insights** — Lighthouse performance + SEO scores (0-100), Core Web Vitals (LCP, CLS, TBT, FCP) with both lab and real-user CrUX field data, LCP fix opportunities ranked by estimated ms savings, Lighthouse SEO pass/fail checks.
14. **Schema Validation** — extracts JSON-LD + microdata from homepage, validates required properties per type (Article, Product, FAQPage, LocalBusiness, BreadcrumbList, HowTo). Reports types found, issues, and successes.
15. **AI Crawler Audit** — checks robots.txt policy for 14 AI crawlers (GPTBot, ChatGPT-User, ClaudeBot, PerplexityBot, Google-Extended, CCBot, Bytespider, FacebookBot, Amazonbot, etc.). Warns about policy gaps (e.g., blocking named bots but allowing CCBot).

**SERP Intelligence** (`utils/seo_serp_intel.py`):

16. **7-Day Regression Alerts** — compares last 7 days vs prior 7 days at query+page level. Detects disappeared entities, position drops >2, CTR collapses (<70% of prior), and click drops >50. Only flags significant entities (>=10 clicks or >=100 impressions in prior period).
17. **AI Overview Monitor** — auto-selects top 10 high-impression low-CTR keywords, batch-checks each against live Google SERPs via DataForSEO advanced endpoint. Reports AI Overview presence, Featured Snippets, and People Also Ask per keyword. Capped at 10 keywords to control cost (~$0.006/audit).

**GA4 Post-Click Intelligence** (`utils/seo_ga4_intel.py`):

18. **Organic Overview** — organic-only sessions, users, bounce rate, engagement rate, avg duration, conversions with current vs prior period deltas.
19. **Tracking Health Check** — compares GSC total clicks vs GA4 organic sessions. Ratio 0.6-1.4 = healthy. Below 0.6 = tracking gap (consent banner, broken tag). Above 1.4 = filter issue (bot traffic).
20. **Landing Page Health** — scores each landing page 0-100 based on bounce rate (>70%: -25), engagement rate (<40%: -25), session duration (<30s: -15), and conversion rate (0: -15). Tags: red (<50), amber (50-75), green (>75). Sorted worst-first.

**Supplementary Integrations:**

- **GBP Audit** — category recommendations, review stats (when Google Business Profile connected).
- **Link Profile** — domain authority, referring domains, backlink health.

### Issue Detection

All analyses auto-inject findings into a unified issues/opportunities list with severity levels (critical/warning/info). Examples:

| Issue Type | Threshold | Severity |
|------------|-----------|----------|
| Low CTR | <1% avg | warning |
| Critically low CTR | <0.5% avg | critical |
| Poor position | >20 avg | warning |
| Invisible position | >50 avg | critical |
| Dead zone keywords | >20 in positions 15-70 | critical |
| Brand dependency | >80% clicks from brand | warning |
| NAP inconsistency | health <90% | warning / <70% critical |
| Traffic drops | >=5 pages losing traffic | critical |
| Cannibalization | >=3 queries with competing pages | warning |
| Content decay | Any pages in sustained decline | warning |
| Poor page speed | Performance <50 | critical / <75 warning |
| Slow LCP | Score <0.5 | critical |
| No schema | No structured data on homepage | warning |
| AI bots blocked | >=10 of 14 crawlers blocked | warning |
| Recent regressions | >=5 alerts in 7 days | critical |
| AI Overview impact | Any checked keywords with AIO | warning |
| Red landing pages | >=3 pages scoring red | critical |
| Tracking gap | GA4/GSC ratio <0.6 | warning |
| Organic traffic drop | Sessions down >=20% vs prior period | critical |

### 6-Tab UI

1. **Dashboard:** SEO Health Score (0-100), issues/opportunities count with severity breakdown, key findings summary, executive narrative.
2. **Audit Results:** NAP health + conflicts; multi-location selector; practice area + brand split; dead-zone keywords (top 50); top-performing keywords; **Page-Level Intelligence** (traffic drops, quick wins, CTR opportunities, content decay, cannibalization); **Technical Health** (PageSpeed/CWV, schema validation, AI crawler audit); **SERP Intelligence** (7-day alerts, AI Overview monitor); **Post-Click Intelligence** (organic overview, tracking health, landing page health scores).
3. **Recovery Plan:** plan type selector (Hybrid, SEO Only, Paid Only, Maintenance/Pause) + industry input; AI-generated 3-phase plan (Months 1-3, 4-6, 7-12) with budget/timeline summary + iCal export.
4. **Audit History:** previous audits listed with config + compare any two with % deltas.
5. **Client Comms:** 5 AI email templates (initial analysis, strategy options, progress update, monthly report, proposal) with tone selector (professional/casual/direct), editable preview, copy/download PDF/save/send via email + communication history table with view.
6. **Reminders:** create follow-ups (type/date/note), email notifications + daily digest option, CRUD table (complete/delete/reschedule), test email + iCal export.

### AI Generation

- **Recovery Plans:** GPT-4-turbo generates 3-phase plans using all audit data (including page-level intelligence, technical findings, and GA4 metrics when available) as context. Template-based fallback if AI unavailable.
- **Client Communications:** GPT-4-turbo generates email content with comparison data for progress reports. 5 templates with 3 tone options. Template-based fallback.
- **Cost tracking:** All AI operations tracked via `utils/cost_tracking.py`.

### Data Storage

Each audit persists to `seo_recovery_audits` with dedicated columns:

| Column | Contents |
|--------|----------|
| `gsc_raw_data` | Filtered keyword data |
| `practice_area_breakdown` | Industry categorization |
| `dead_zone_keywords` | Positions 15-70 opportunities |
| `brand_vs_nonbrand` | Traffic split |
| `issues_identified` | Unified issues list |
| `opportunities` | Unified opportunities list |
| `audit_config` | User configuration |
| `intelligence_data` | Phase 1: traffic drops, quick wins, CTR opps, content decay, cannibalization |
| `technical_data` | Phase 2: PageSpeed, schema, AI bots |
| `serp_intel_data` | Phase 3: 7-day alerts, AIO monitor |
| `ga4_intel_data` | Phase 4: organic overview, tracking health, landing page health |

## Why It Matters

Gives agencies a repeatable emergency workflow to diagnose SEO performance issues across the full funnel — from SERP visibility (GSC) through technical health (PageSpeed, schema, AI crawlers) to post-click experience (GA4). Generates credible recovery plans grounded in specific page-level findings, and communicates clearly with clients using real metrics and structured follow-up.

## Requirements

- **Required:** Google Search Console (OAuth)
- **Recommended:** Link Profile (snapshot), Google Analytics 4 (OAuth)
- **Optional:** Google Ads (search volume enrichment), Google Business Profile (OAuth), DataForSEO (AI Overview monitoring)
- **AI:** OpenAI API (recovery plans + client communications)
- **Email:** SendGrid (client comms + reminder notifications)
- **Pip:** `extruct` (schema extraction)

## Cost Per Audit

| Component | Cost |
|-----------|------|
| GSC analyses (Phases 1 + alerts) | Free |
| PageSpeed / Schema / AI Bots | Free |
| GA4 analyses | Free |
| AI Overview Monitor (DataForSEO) | ~$0.006 (optional, 10 keywords) |
| Recovery Plan generation (OpenAI) | ~$0.02-0.05 |
| Client Communication (OpenAI) | ~$0.01-0.03 |

## Backend Modules

| Module | Purpose |
|--------|---------|
| `utils/seo_intelligence.py` | GSC page-level intelligence (5 analyses) |
| `utils/seo_technical.py` | PageSpeed, schema validation, AI crawler audit |
| `utils/seo_serp_intel.py` | SERP alerts + AI Overview monitoring |
| `utils/seo_ga4_intel.py` | GA4 post-click diagnostics |
| `utils/cost_tracking.py` | Usage tracking for AI + DataForSEO calls |
