# Features

AlmaSEO is a comprehensive SEO content platform with **134 features** organized across content creation, client management, content intelligence, and automation.

Browse by category below, or use the search bar to find a specific feature.

---

## Content Creation

*The engine that powers article generation, from topic selection through publishing.*

### [Content Creation](content-creation/index.md) `Core/Free`

The engine that powers everything

| Feature | Tier | Description |
|---------|------|-------------|
| [Generate Content Brief Only](content-creation/generate-content-brief-only.md) | Agency | Toggle option that outputs a detailed content brief for human writers instead of a full AI-genera... |
| [Article Types](content-creation/article-types.md) | Core/Free | 11 content types, each with specialized logic |
| [Content Inventory](content-creation/content-inventory.md) | Pro | See everything that exists — before you write |
| [Content Output](content-creation/content-output.md) | Core/Free | What gets generated with every article |
| [Publishing & Export](content-creation/publishing-export.md) | Core/Free | Deliver content to ANY platform |
| [Article Creation Form](content-creation/article-creation-form.md) | Core/Free | The central interface where users configure all settings for a new article. Houses tone, length, ... |
| [Post Details](content-creation/post-details.md) | Core/Free | The post-creation hub where users view, validate, and take action on generated content. Displays ... |
| [GBP Testimonials in Generated Articles](content-creation/gbp-testimonials-in-generated-articles.md) | Pro | When a blog article is generated for a site that has Google Business Profile (GBP) connected, Alm... |

---

## Client Management

*Per-site command center with business info, Google integrations, analytics, and monitoring.*

### [Client Profile](client-profile/index.md) `Agency`

The command center for each site/client. Every site added to AlmaSEO gets its own Client Profile containing business information, integrations, SEO tools, analytics, and content management. This is where the "intelligence" about a client lives — the data that feeds into content generation, E-E-A-T signals, and personalized recommendations. Agencies managing multiple clients see each as a card on the main dashboard.

| Feature | Tier | Description |
|---------|------|-------------|
| [Overview](client-profile/overview.md) | Pro | Dashboard showing profile setup status and integration health at a glance. Displays Profile Compl... |
| [Business Information](client-profile/business-information.md) | Core/Free | Core business details that power content personalization and E-E-A-T signals. Fields include: Com... |
| [Locations](client-profile/locations.md) | Pro | Manages multiple business locations with individual NAP (Name, Address, Phone) data. Each locatio... |
| [NAP Shield](client-profile/nap-shield.md) | Agency | Monitors a business’s Name, Address, Phone (NAP) consistency across the web by discovering citati... |
| [Social Profiles](client-profile/social-profiles.md) | Pro | A centralized place to store and manage a client’s social media profile links so they’re easy to ... |
| [Services & Areas](client-profile/services-areas.md) | Pro | A Client Profile hub to define what services the business offers and the geographic areas it targ... |
| [Wordpress Settings](client-profile/wordpress-settings.md) | Core/Free | Consolidated WordPress connection + diagnostics tab for a client site. 

1) Connection Status (to... |
| [Google Services](client-profile/google-services.md) | Pro | Client Profile parent dropdown that centralizes all Google-related connections, account/property ... |
| [Content Hub](client-profile/content-hub.md) | Pro | Client Profile parent dropdown for end-to-end blog/content management. The Content Hub is a three... |
| [Ownership Tracker](client-profile/ownership-tracker.md) | Agency | Password-protected, multi-tab spreadsheet embedded in Client Profile for documenting the credenti... |
| [Infrastructure Scan](client-profile/infrastructure-scan.md) | Pro | Client Profile parent dropdown for automated infrastructure monitoring. Infrastructure Scan runs ... |
| [Website Analysis](client-profile/website-analysis.md) | Pro |  |
| [Backlinks](client-profile/backlinks.md) | Pro | Client Profile parent dropdown for backlink management. Provides an end-to-end system for importi... |
| [Content Automation](client-profile/content-automation.md) | Pro | Client Profile tab for planning, configuring, and monitoring a per-site automated content publish... |
| [Activity & Logs](client-profile/activity-logs.md) | Pro/Agency | Unified, per-site timeline inside Client Profile (last tab) that shows everything that happened f... |
| [Client Work Report Email](client-profile/client-work-report-email.md) | Pro/Agency | Inside the Client Profile → Activity & Logs tab, users can select reportable timeline entries (or... |

---

## Content Intelligence

*AI-powered content strategy — recommendations, data sources, and the Content Authority Engine.*

### [Content Intelligence](content-intelligence/index.md) `Pro`

A content strategist in 30 seconds

| Feature | Tier | Description |
|---------|------|-------------|
| [AI Content Recommendations](content-intelligence/ai-content-recommendations.md) | Pro | Full content strategy from one button click |
| [Intelligence Data Sources](content-intelligence/intelligence-data-sources.md) | Core/Free | What feeds the recommendation engine |
| [Content Authority Engine](content-intelligence/content-authority-engine.md) | Core/Free | Proprietary writing intelligence system that powers all content generation. Eliminates AI fingerp... |

---

## SEO & Analysis

*Technical SEO audits, structured data, and schema management.*

### [SEO Operations](seo-operations/index.md) `Agency`

Audits, health checks, optimization

---

### [Structured Data (Schema)](structured-data-schema/index.md) `Pro`

Umbrella capability for generating, validating, detecting, and delivering http://Schema.org structured data across AlmaSEO. This covers multiple schema systems including on-demand generators, export-time embedding, WordPress injection, editor integrations, and background detection/scoring.

| Feature | Tier | Description |
|---------|------|-------------|
| [Structured Data Dashboard & WordPress Injection](structured-data/structured-data-dashboard-wordpress-injection.md) | Agency | API-driven structured data system with optional dashboard UI (behind SD_ENABLE=1) that can genera... |

---

## Automation

*Automated content scheduling, publishing pipeline, and operational monitoring.*

### [Automation Center](automation-center/index.md) `Pro`

Global system dashboard for automation operations across all sites (/automation). Provides a consolidated view of queue health, worker status, capacity, and system mode (read-only badge). Also surfaces quality scores as color-coded badges and supports job/DLQ review with admin-only controls.

Key sections include: Automation System Status badges, operational health tiles (job-type metrics), Automation Insights KPIs, Recent Jobs, Dead Letter Queue, site links, and system statistics.

Quick Actions:
- “View X Scheduled Posts” scrolls to the Recent Jobs panel.
- Admin-only queue management controls (Pause, Resume, Retry All, Clear Pending) have working backend endpoints.

Access control note: DLQ, queue controls, and runtime flags are admin-only.

---

### [Content Automation](content-automation/index.md) `Pro`

Client Profile tab for planning, configuring, and monitoring a per-site automated content publishing pipeline.

UI structure (sub-tabs):
- Content Planning: generate topic ideas, add custom topics, reorder topics, and select which ones to schedule. On save, topics are scored for similarity, duplicates can be blocked or overridden by confirmation, and accepted topics are stored as the plan.
- Settings: start date, schedule duration (weeks), draft vs auto-publish, preferred publish time, and post-ready email notifications. Posting frequency and daily caps are user-configurable here.
- Monitoring: recent jobs, job detail, queue health, and failed job review (DLQ). Jobs created from Content Planning are traceable and show a “Planned” badge plus the original topic/source in job details. Completed jobs with a WordPress post show a “Generate” action to open the featured image generator modal and upload an image directly to the post.

Execution pipeline (when a topic runs): plan is saved → scheduler bridge converts due planned topics into automation_jobs → guardrail checks → AI article generation (can include GBP review testimonials if available) → quality scoring (visible as color-coded badges) → WordPress publish (draft or live) → optional IndexNow submission → optional email notification → activity/log updates.

Access control note: DLQ, queue controls, and runtime flags are admin-only.

| Feature | Tier | Description |
|---------|------|-------------|
| [Topic Scheduling](client-profile/topic-scheduling.md) | Pro | Content Planning sub-tab surface for building a per-site publishing plan. Users can generate topi... |
| [Automation Settings](client-profile/automation-settings.md) | Pro | Settings sub-tab surface for per-site automation configuration. Users toggle content automation o... |
| [Monitoring](client-profile/monitoring.md) | Pro | Monitoring sub-tab surface for observing automation activity for a single site. Shows recent jobs... |
| [Content Pipeline](client-profile/content-pipeline.md) | Pro | End-to-end automation workflow that generates and publishes content for a site.

Pipeline steps:
... |
| [Guardrails & Safety](client-profile/guardrails-safety.md) | Pro | Reliability and safety mechanisms that prevent over-publishing, duplicates, and runaway failure l... |
| [Monitoring & Logs](client-profile/monitoring-logs.md) | Pro | Operational visibility for automation across sites. Provides per-job logs and system health indic... |

---

## Platform

*Cross-cutting platform features — AI chat, WordPress connector, site management.*

### [Alma AI Chat — Global AI Assistant](alma-ai-chat-global-ai-assistant/index.md) `Pro/Agency`

Floating chat widget available on every page that lets users ask plain-English questions about their live AlmaSEO platform data. Powered by GPT-4o-mini with tool calling to query internal databases plus live Google Analytics and Google Search Console data in real time, with persistent multi-turn conversation history.

---

### [AlmaSEO WordPress Connector Plugin](almaseo-wordpress-connector-plugin/index.md) `Pro`

A WordPress plugin that acts as a secure bridge between a WordPress site and the AlmaSEO platform. It enables two-way communication so AlmaSEO can manage, publish, and optimize content on the connected WordPress site.

Core capabilities:
1) Secure authentication: generates/manages WordPress Application Passwords for API access; supports auto-connect via a shared secret; stale password detection clears orphaned credentials.
2) SEO metadata management: writes title, description, keywords, Open Graph, Twitter cards, canonical URLs, robots directives via REST API; compatible with AIOSEO (Free + Pro), Yoast SEO, and Rank Math.
3) Site capabilities reporting: endpoint exposes post types, taxonomies, REST endpoints, and whether Application Passwords/custom fields are enabled.
4) Connection verification: endpoint confirms plugin is active, checks plugin version, and returns site info (name, URL, WordPress version).
5) SEO Playground: meta box in post/page editor for SEO Title, Meta Description, Focus Keyword, Schema Type, and SEO Notes; character counters and live Google snippet preview.
6) AI-powered features (when connected): Post Intelligence (AI content summary), Keyword Intelligence (intent/difficulty), and Re-Optimization Alerts for aging posts.
7) SEO status detection: reports which SEO plugin is installed, version, Pro/free, and capabilities so AlmaSEO can write metadata correctly.
8) Security: CORS restricted to http://api.almaseo.com; secret-based endpoint protection; nonce verification; admin-only permission checks; timing-safe secret comparison (hash_equals).

---

### [Site Management](site-management/index.md) `Agency`

Multi-site dashboard and client management

---

### [Analytics & Insights](analytics-insights/index.md) `Agency`

GSC + GA4 performance intelligence

---

### [Backlinks & Outreach](backlinks-outreach/index.md) `Agency`

Discovery, outreach, verification

---


## Already Documented

- [Alma AI Chat](alma-ai-chat.md) — Global AI chat assistant with live data access across all your sites

