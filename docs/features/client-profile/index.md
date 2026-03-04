---
title: "Client Profile"
slug: "client-profile"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "CP"
last_updated: "2026-03-04"
---

# Client Profile

## Overview

Client Profile is the per-site command center in AlmaSEO. Every site added to the platform gets its own Client Profile — a single page at `/site/<id>/profile` that houses everything about that site: business information, Google integrations, content management, SEO analysis tools, backlink tracking, automation settings, infrastructure monitoring, and activity logs.

This is where the "intelligence" about a client lives. The business name, services offered, industry type, locations, and connected Google accounts stored here feed directly into content generation (E-E-A-T signals), Content Intelligence (recommendation targeting), automation (topic selection), and every other feature that needs to know about the business.

Agencies managing multiple clients see each site as a card on the main dashboard. Clicking into any site opens its full Client Profile with a sidebar navigation and 26 section panels organized into collapsible groups.

---

## What It Does

### Sidebar Navigation

The Client Profile uses a fixed sidebar with collapsible groups. Only one section panel is visible at a time. The sidebar is organized into these groups:

#### Business Setup

The foundation — business data that powers everything else.

| Section | What It Stores |
|---------|---------------|
| **[Business Information](business-information.md)** | Company name, owner, about us, phone, email, industry type, business hours, services offered, service areas, awards. Logo upload (PNG/JPG/SVG, max 2MB). |
| **[Locations](locations.md)** | Multi-location NAP (Name, Address, Phone) management. Each location has its own address, phone, hours, Google Maps URL, and optional GBP connection. Supports Service Area Businesses (no public address). Bulk CSV import/export. |
| **[NAP Shield](nap-shield.md)** | Monitors business name, address, and phone consistency across web citations (Google, Yelp, YP, etc.). Health score (0-100), consistent/inconsistent/missing counts, per-citation detail with exact values found vs. master data. |
| **[Social Profiles](social-profiles.md)** | Centralized storage for Facebook, Twitter/X, Instagram, LinkedIn, YouTube, Pinterest, and TikTok URLs. Used by the content generator for accurate social links in articles. |
| **[Services & Areas](services-areas.md)** | Services the business offers and geographic areas it serves. This is the single most impactful field for Content Intelligence — it transforms generic recommendations into business-specific ones. |
| **Branding** | Primary and secondary brand colors, brand voice (Professional/Friendly/Authoritative/Conversational), and slogan. Colors apply to UI theming; voice feeds into content generation tone. |
| **Mailchimp Settings** | Connect a Mailchimp account, select an email list, and configure campaigns to send published articles as email blasts. |

#### WordPress Integration

| Section | What It Stores |
|---------|---------------|
| **[WordPress SEO Plugin](wordpress-seo-plugin.md)** | Auto-detected SEO plugin (AIOSEO, Yoast, Rank Math, SEOPress, The SEO Framework) with manual override dropdown. Health check for API access, metadata writing, and schema support. |
| **WordPress Settings** | WordPress username, Application Password, connection status (Connected/Error/Not configured), and test connection button. |
| **[AlmaSEO for WordPress](almaseo-for-wordpress.md)** | Plugin status for AlmaSEO Connector or SEO Playground — installed, active, version, download links, and upgrade path. |

#### Google Services

Five Google integrations, each with its own tab.

| Section | What It Provides |
|---------|-----------------|
| **[Search Console](search-console.md)** | Query metrics (impressions, clicks, CTR, average position), top performing queries, indexed pages count, and coverage issues. Feeds into Content Intelligence for gap analysis and SEO Recovery 911 for audits. |
| **[Analytics](analytics.md)** | GA4 property metrics — user engagement, traffic by source, page performance, goal tracking. Supports custom queries and period comparison. |
| **[Business Profile](business-profile.md)** | Google Business Profile data — location status, reviews (with AI draft responses), photos, search queries, and performance metrics. Uses 3 separate Google APIs. |
| **[Google Ads](google-ads.md)** | Ad performance metrics when a Google Ads account is connected. |
| **[Content AI](content-ai.md)** | Google Natural Language API integration for sentiment analysis, entity extraction, syntax analysis, and content quality scoring. |

#### Content Hub

Post management across the full content lifecycle.

| Section | What It Shows |
|---------|--------------|
| **Published Posts** | All published articles with topic, date, word count, author, and GSC submission status. Search, filter (by date range, GSC status), and sort (date, word count, alphabetical). |
| **Scheduled Posts** | Upcoming automated posts in chronological order with duplicate risk scoring (high/medium/low) and similarity to existing content. |
| **Drafts** | Draft articles awaiting review, with last updated timestamp and word count. |

#### Ownership Tracker

**[Ownership Tracker](ownership-tracker.md)** — a password-protected, multi-tab spreadsheet for documenting the credentials, accounts, and services that make up a client's digital infrastructure. Stores domain registrar logins, hosting accounts, email providers, social media accounts, and service provider credentials behind a master password with encrypted storage.

#### Website Infrastructure

Automated scanning of the site's technical foundation.

| Section | What It Scans |
|---------|--------------|
| **[Scan Overview](scan-overview.md)** | Summary of all infrastructure checks — domain, SSL, hosting, email status at a glance. |
| **[Domain & DNS](domain-dns.md)** | Domain registrar, DNS records (A, MX, TXT, CNAME), domain expiration date, and propagation status. |
| **[Hosting](hosting.md)** | Hosting provider identification, server IP, uptime monitoring, and page speed metrics. |
| **[SSL & Security](ssl-security.md)** | SSL certificate status and expiration, security score, mixed content warnings, HTTPS enforcement. |
| **[Email Providers](email-providers.md)** | Email provider detection, SPF/DKIM/DMARC configuration, and deliverability assessment. |

Scans run on a scheduled basis (daily/weekly) with critical alert notifications and digest email reports.

#### Website Analysis

AI-powered analysis tools for UX, SEO health, and search visibility.

| Section | What It Does |
|---------|-------------|
| **[First Impression Tool](first-impression-tool.md)** | Visual/UX analysis of the website — eye journey, clutter, layout, colors, typography, conversion elements, and mobile experience. Does **not** use location/address data (visual analysis only). |
| **[GEO/AI Search Optimizer](geo-ai-search-optimizer.md)** | Analyzes the site's readiness for AI search engines (ChatGPT, Claude, Perplexity) — schema markup, content structure, authority signals, and citation-friendly formatting. Uses location data for local SEO signals. |
| **[SEO Recovery 911](seo-recovery-911.md)** | Comprehensive SEO audit and recovery planning for ranking crises. GSC-powered analysis, dead zone detection (keywords stuck in positions 15-70), NAP health check, phased recovery plans (SEO/Paid/Hybrid), and professional client communications. Requires GSC connection. |

#### Backlinks

End-to-end backlink management pipeline.

| Section | What It Does |
|---------|-------------|
| **[Backlinks Overview](backlinks-overview.md)** | Total backlinks, referring domains, live links, new this month. Import from CSV (supports Google Search Console, Ahrefs, Semrush, Moz, Majestic formats). Bulk verification. |
| **[Opportunities](opportunities.md)** | Websites that link to competitors but not to you, ranked by domain authority. |
| **[Outreach](outreach.md)** | Kanban-style pipeline (To Do → Contacted → Won) with email campaigns, outreach sequences, email templates, and conversation tracking. |
| **[Live Links](live-links.md)** | All verified live backlinks with status, last verified date, domain authority, and linking page title. |

#### Content Automation

Per-site automated content publishing pipeline.

| Section | What It Does |
|---------|-------------|
| **[Topic Scheduling](topic-scheduling.md)** | Build a publishing plan — generate topic ideas, add custom topics, reorder, and select which ones to schedule. Similarity scoring prevents duplicates. |
| **[Automation Settings](automation-settings.md)** | Start date, schedule duration, draft vs. auto-publish, preferred publish time, posting frequency, daily caps, and email notifications. |
| **[Monitoring](monitoring.md)** | Recent jobs, job details, queue health, and failed job review (dead letter queue). Completed jobs with WordPress posts can generate featured images directly. |
| **[Content Pipeline](content-pipeline.md)** | End-to-end execution flow: plan → scheduler → guardrails → AI generation → quality scoring → WordPress publish → IndexNow → email notification → activity log. |
| **[Guardrails & Safety](guardrails-safety.md)** | Over-publishing prevention, duplicate blocking, circuit breakers, and failure rate limits. |
| **[Monitoring & Logs](monitoring-logs.md)** | Per-job logs and system health indicators across all automation activity. |

#### Activity & Logs

| Section | What It Does |
|---------|-------------|
| **[Activity & Logs](activity-logs.md)** | Unified, chronological timeline of everything that happened for the site — content published, settings updated, Google connections established, posts indexed, backlinks checked, scans completed, automations triggered. Filterable and searchable. |
| **[Client Work Report Email](client-work-report-email.md)** | Select reportable timeline entries (or auto-select the last 7 days), compose a branded email, and send a professional work report to the client. |

#### Settings

Site configuration — site name (read-only), URL, site type (WordPress/Static), WordPress connection status. Includes a danger zone with site deletion (two-step confirmation).

### Profile Completeness

The Overview tab calculates a completion percentage based on 21 fields across 5 categories:

| Category | Fields Tracked |
|----------|---------------|
| **Business Information** (9) | Business name, about us, phone, email, address, business hours, services offered, service areas, industry type |
| **Branding** (2) | Logo, slogan |
| **Social Profiles** (1) | At least one social URL |
| **WordPress Integration** (4) | Credentials set, connection verified, SEO plugin detected, AlmaSEO plugin active |
| **Google Services** (5) | Search Console, Analytics, Business Profile, Google Ads, Content AI |

Higher completeness directly improves content quality — more filled fields mean stronger E-E-A-T signals, more targeted recommendations, and more personalized articles.

---

## Why It Matters

- **The intelligence layer** — every field in Client Profile makes the AI smarter. Business name, services, industry, and about us text are injected into every article as E-E-A-T signals. Without profile data, content is generic. With it, content reads like it was written by someone who knows the business.
- **Single source of truth** — one place to manage all business data, Google connections, WordPress credentials, and content for each site. No jumping between tools or spreadsheets.
- **Multi-client management** — agencies managing dozens of sites see each client as a card on the dashboard, then drill into the full profile. Each site is isolated — its own data, its own integrations, its own content pipeline.
- **Feeds every feature** — Content Creation reads business info for E-E-A-T. Content Intelligence reads GSC and services for recommendations. Automation reads settings for scheduling. NAP Shield reads locations for consistency checks. Nothing works in isolation.
- **Progressive value** — the more data connected (Google services, business details, locations), the more powerful every downstream feature becomes. Profile completeness is a direct indicator of platform value.
- **Client accountability** — Activity & Logs plus Client Work Report Email create an audit trail and professional reporting workflow for agencies to demonstrate value to clients.

---

## How to Use It

### Accessing a Client Profile

1. From the main dashboard, click on any site card.
2. The Client Profile opens at the **Overview** tab showing completeness and integration health.
3. Use the **sidebar** to navigate between sections. Collapsible groups expand to show child tabs.

### Setting Up a New Site

The recommended setup order for maximum value:

1. **Business Information** — fill in company name, owner, about us, phone, email, industry type. This is the minimum for quality content generation.
2. **Services & Areas** — add the services offered and geographic service areas. This is the single biggest improvement for Content Intelligence recommendations.
3. **Locations** — add the primary business location (or toggle Service Area Business for mobile/home-based businesses).
4. **WordPress Settings** — connect WordPress credentials (or install the AlmaSEO Connector Plugin for auto-connect).
5. **Google Services** — connect Search Console, Analytics, and Business Profile via OAuth for full data integration.
6. **Social Profiles** — add social media URLs for inclusion in generated content.
7. **Branding** — upload logo, set brand colors and voice.

### Managing Content

- Use **Content Hub → Published Posts** to review all published articles with search, filter, and sort.
- Use **Content Hub → Scheduled Posts** to monitor upcoming automated posts and their duplicate risk scores.
- Use **Content Hub → Drafts** to find articles awaiting review.

### Monitoring & Reporting

- **Activity & Logs** shows a complete timeline of all site activity.
- **Client Work Report Email** lets you select entries and send a branded report to the client.
- **Infrastructure Scan** runs automated checks on domain, SSL, hosting, and email configuration.
- **Backlinks** tracks link building progress from import through outreach to verified live links.

---

## Key Settings / Options

### Data That Powers Other Features

| Field | Where It's Used |
|-------|----------------|
| `services_offered` | Content Intelligence (recommendation targeting), Content Creation (E-E-A-T, topic relevance) |
| `business_name` | Content Creation (E-E-A-T author signals), NAP Shield (master data) |
| `about_us` | Content Creation (E-E-A-T experience/expertise signals, tenure extraction) |
| `industry_type` | Content Creation (authority title mapping — Attorney, Specialist, Technician, etc.) |
| `locations` (primary) | Content Creation (local SEO content), NAP Shield (consistency checks), GEO/AI Optimizer |
| `brand_voice` | Content Creation (writing tone), Automation (default tone for scheduled posts) |
| Google Search Console | Content Intelligence (gap analysis, search visibility), SEO Recovery 911 (audit data) |
| Google Business Profile | Content Intelligence (search queries, review mining), Content Creation (GBP testimonials) |
| Google Analytics | Alma AI Chat (live traffic queries), Analytics dashboard |
| `wp_user` + `wp_app_password` | Content publishing, metadata writing, plugin detection |

### Site Types

| Type | Publishing | Content Inventory | Export |
|------|-----------|-------------------|--------|
| **WordPress** | Direct publish via REST API | WordPress Content Pull | All formats |
| **Static** | No direct publish | Sitemap & scrape discovery | All formats (export only) |

---

## Notes / Edge Cases

- **Profile completeness drives quality** — this isn't just a progress bar. Each filled field directly feeds into AI prompts, E-E-A-T injection, and recommendation targeting. A 90% complete profile produces measurably better content than a 30% profile.
- **Services Offered is the most impactful field** — it transforms Content Intelligence from generic topic suggestions to business-specific strategy. Always fill this first after the basics.
- **Locations table is the modern data model** — business address data is stored in the `locations` table, not the `sites` table. If a site shows a "Virtual Location" notice, it has legacy address data that should be migrated to a Location record.
- **GBP integration is fragile** — it uses 3 separate Google APIs with specific data formats. Do not modify GBP-related code without explicit instruction.
- **Google OAuth tokens are per-service** — Search Console, Analytics, Business Profile, Ads, and Content AI each have their own OAuth connection. Connecting one does not connect the others.
- **Site deletion is permanent** — the Settings tab includes a danger zone with two-step confirmation. All site data, posts, integrations, and history are permanently removed.
- **Activity logging is comprehensive** — nearly every action (content published, settings changed, connections established, scans completed) is logged to the Activity & Logs timeline automatically.

### Sub-features

- **[Overview](overview.md)** *(Pro)* — Profile completeness and integration health dashboard.
- **[Business Information](business-information.md)** *(Core/Free)* — Core business details for content personalization.
- **[Locations](locations.md)** *(Pro)* — Multi-location NAP management with SAB support.
- **[NAP Shield](nap-shield.md)** *(Agency)* — Web citation consistency monitoring.
- **[Social Profiles](social-profiles.md)** *(Pro)* — Social media URL storage.
- **[Services & Areas](services-areas.md)** *(Pro)* — Services offered and geographic targeting.
- **[Google Services](google-services.md)** *(Pro)* — Google integrations hub.
- **[Content Hub](content-hub.md)** *(Pro)* — Published, scheduled, and draft post management.
- **[Ownership Tracker](ownership-tracker.md)** *(Agency)* — Password-protected credentials vault.
- **[Infrastructure Scan](infrastructure-scan.md)** *(Pro)* — Automated domain, SSL, hosting, and email scanning.
- **[Website Analysis](website-analysis.md)** *(Pro)* — First Impression, GEO/AI Optimizer, SEO Recovery 911.
- **[Backlinks](backlinks.md)** *(Pro)* — Import, verify, outreach, and track backlinks.
- **[Content Automation](content-automation.md)** *(Pro)* — Automated content publishing pipeline.
- **[Activity & Logs](activity-logs.md)** *(Pro/Agency)* — Unified site activity timeline.
- **[Client Work Report Email](client-work-report-email.md)** *(Pro/Agency)* — Branded client reporting.
- **[WordPress SEO Plugin](wordpress-seo-plugin.md)** *(Pro)* — SEO plugin detection and configuration.
- **[AlmaSEO for WordPress](almaseo-for-wordpress.md)** *(Pro)* — AlmaSEO plugin health and status.
