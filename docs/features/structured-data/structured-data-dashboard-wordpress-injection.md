# Structured Data Dashboard & WordPress Injection

**Tier:** Agency | **Type:** Automation / Background

!!! tip "Key Insight"
    This is the “enterprise” schema pipeline: stored snippets, coverage metrics, and automated injection. It’s a foundation for scaling schema across many posts without manual copy/paste.

## Overview

API-driven structured data system with optional dashboard UI (behind SD_ENABLE=1) that can generate schema snippets, track coverage, store results, and inject schema into WordPress.

User surface:
- API routes at /api/structured-data/*.
- When enabled, dashboard at /api/structured-data/dashboard/<site_id> shows metrics, coverage %, and snippet table.
- Not prominently surfaced in main navigation.

Generation & delivery:
- On-demand and queued generation (jobs like sd_generate_post, sd_inject_post).
- Uses utils/structured_http://data.py generator (separate from other generators).
- Stores snippets in sd_snippets (per-post) and sd_site_snippets (site-wide).
- Tracks coverage in sd_coverage.
- Injects into WordPress via wp_content_http://injector.py using <!-- alma:sd --> markers.

Schema types:
- BlogPosting / Article
- FAQPage (extracts Q&A from HTML patterns)
- HowTo (extracts steps from <ol> and “Step X:” patterns)
- BreadcrumbList
- Organization
- WebSite (SearchAction)

Primary inputs:
- Post HTML (for extraction)
- Env vars (SD_ORG_NAME, SD_ORG_LOGO_URL, SD_SITE_SEARCH_URL, SD_TYPES)
- WP post metadata (REST API)
- Word count, author, publish date

## Why It Matters

Gives WordPress workflows a scalable way to generate and inject structured data across posts, with coverage tracking and repeatable automation.

## Requirements

- **Integrations:** Wordpress API
- **Compatibility:** Wordpress

## Access Control

**Permission Mode:** Configurable per client

## Target Audience

Agencies, Freelancers

