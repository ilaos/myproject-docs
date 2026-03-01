# Feature Dependencies & Integration Map

This page documents verified dependencies between AlmaSEO features and their required integrations. Use this when planning which features to enable for a site — it tells you exactly what needs to be connected before a feature will work.

!!! info "How to Read This Page"
    **Hard dependency** = the feature cannot function without it. **Optional** = the feature works without it but gains extra capability when available. **Enhancement** = adds supplementary data but the core feature is unaffected.

---

## Integration Requirements by Feature

### OpenAI API (48 features)

The AI backbone powering content generation, analysis, and recommendations. Nearly every content-producing feature requires an active OpenAI API connection.

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| Content Creation (all article types) | Hard | Powers all AI content generation |
| Content Authority Engine | Hard | Humanization, E-E-A-T, structural depth |
| AI Content Recommendations | Hard | GPT-4o-mini generates strategy |
| First Impression (UX Analysis) | Hard | GPT-4o Vision scores 6 UX categories |
| GEO/AI Search Optimizer | Hard | AI evaluates entity clarity and citation-worthiness |
| Alma AI Chat | Hard | GPT-4o-mini with tool calling |
| Content Automation pipeline | Hard | Generates articles for scheduled topics |
| SEO Recovery 911 | Hard | AI analysis of GSC data patterns |

### WordPress API (24 features)

Required for any feature that reads from or publishes to a WordPress site. The [AlmaSEO WordPress Connector Plugin](almaseo-wordpress-connector-plugin/index.md) must be installed and connected.

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| Auto-Publish to WordPress | Hard | Cannot publish without connection |
| WordPress Content Pull | Hard | Reads existing posts/pages for inventory |
| Content Automation pipeline | Hard | Publishes generated articles |
| WordPress Settings | Hard | Connection status + diagnostics |
| SEO Metadata (Yoast/AIOSEO/RankMath) | Hard | Writes meta via REST API |
| Structured Data WordPress Injection | Hard | Injects schema via API |
| WordPress Categories | Hard | Syncs category taxonomy |
| Content Hub (Published/Drafts/Scheduled) | Hard | Reads post status from WP |

### Google Search Console (7 features)

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| SEO Recovery 911 | **Hard** | Cannot run without GSC — primary data source |
| AI Content Recommendations | Hard | GSC queries feed the recommendation engine |
| Search Console Indexing | Hard | Submits URLs for indexing |
| Content Gap Analysis | Hard | Identifies keyword opportunities from GSC data |
| Analytics (Search Performance) | Hard | GSC impressions, clicks, CTR, position |
| Intelligence Data Sources | Optional | Enriches recommendations when available |
| Content Hierarchy Warnings | Optional | Uses GSC data to detect cannibalization |

### Google Business Profile (6 features)

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| NAP Shield | **Hard** | GBP data is ground truth for NAP consistency |
| GBP Search Queries → AI Recommendations | Hard | Feeds local search queries into content strategy |
| Reviews → Content Mining | Hard | Mines review themes for blog topics |
| GBP Testimonials in Articles | Hard | Embeds real 5-star reviews in generated content |
| Business Profile dashboard | Hard | Displays metrics, reviews, photo stats |
| SEO Recovery 911 | Enhancement | Adds GBP data if available, works without it |

### Google Analytics / GA4 (3 features)

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| Analytics & Insights | Hard | GA4 traffic, engagement, conversion data |
| Alma AI Chat (analytics queries) | Optional | Can answer GA4 questions when connected |
| Overview dashboard | Optional | Shows traffic trends when available |

### SendGrid (9 features)

| Feature | Dependency Type | Notes |
|---------|----------------|-------|
| Publication Report Email | Hard | Sends post-publish notification |
| Client Work Report Email | Hard | Sends activity summary to clients |
| Post-Ready Email Notifications | Hard | Alerts when automation completes a post |
| Mailchimp Article Blast | Hard | Distributes content via email |

---

## Feature-to-Feature Dependencies

These are cases where one AlmaSEO feature requires another AlmaSEO feature to function.

### Verified Hard Dependencies

```
Content Automation ──────→ Content Creation (article generation engine)
                  ──────→ WordPress API (publish target)
                  ──────→ OpenAI API (AI generation)

GEO/AI Search Optimizer ─→ Schema Generator (evaluates structured data)
                        ─→ Structured Data system (schema detection + scoring)

AI Content Recommendations → Intelligence Data Sources (feeds the engine)

Search Console Indexing ──→ Google Search Console (API requirement)

Structured Data Dashboard → WordPress Connector Plugin (injection target)
```

### Verified Optional Dependencies

```
First Impression ·········→ Schema Generator (only in GEO mode, not core UX)
                 ·········→ SEO Recovery data (reads if exists, works without)

Content Authority Engine ··→ GBP Reviews (includes testimonials when available)

AI Recommendations ········→ GBP Search Queries (enriches when connected)
                   ········→ Google Search Console (enriches when connected)
```

### Previously Claimed but Incorrect

These were listed as dependencies but verified against the codebase as **not required**:

| Claimed | Actual | Why |
|---------|--------|-----|
| First Impression → SEO Recovery 911 | Not a dependency | FI only reads cached SEO Recovery data if it happens to exist — no import, no API call, no failure if absent |
| SEO Recovery → GBP | Not a dependency | GBP data optionally enriches the report but SEO Recovery runs entirely on GSC data |
| SEO Recovery → Google Ads | Not a dependency | Google Ads data is optional enrichment shown in a separate section; core audit is GSC-only |

---

## What Do I Need to Enable Feature X?

Quick reference for common setup questions.

### "I want to use Content Automation"
1. OpenAI API key configured
2. WordPress site connected via Connector Plugin
3. At least one topic saved in Content Planning
4. Automation enabled in Settings sub-tab

### "I want AI Content Recommendations"
1. OpenAI API key configured
2. At least one Intelligence Data Source connected (WordPress content, GSC, or GBP)
3. More sources = better recommendations

### "I want First Impression reports"
1. OpenAI API key configured
2. A valid site URL
3. (Optional) For GEO mode: Schema Generator runs automatically as part of the analysis

### "I want SEO Recovery 911"
1. OpenAI API key configured
2. Google Search Console connected and verified
3. (Optional) GBP connected for NAP consistency section

### "I want NAP Shield"
1. Google Business Profile connected
2. Business Information filled in (name, address, phone)
3. Locations configured (for multi-location businesses)

### "I want Structured Data on my WordPress site"
1. WordPress Connector Plugin installed
2. Agency tier (for Dashboard + Injection features)
3. Pro tier sufficient for Schema Generator and detection/scoring

---

## Integration Coverage Summary

| Integration | Features Using It | Required Setup |
|-------------|-------------------|----------------|
| OpenAI API | 48 | API key in platform settings |
| None (standalone) | 45 | No external connection needed |
| WordPress API | 24 | Connector Plugin installed + connected |
| Google APIs (GSC + GA4 + GBP + Ads) | 23 | OAuth connection per service |
| SendGrid | 9 | API key in platform settings |

**Total features:** 134 (some use multiple integrations)
