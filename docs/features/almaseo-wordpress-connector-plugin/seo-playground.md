# SEO Playground (WordPress On-Site SEO Toolkit)

**Tier:** Core/Free (base) + Pro (advanced modules) | **Status:** Shipped | **Type:** User-Facing UI + Integration

!!! tip "Key Insight"
    This is what makes the plugin worth installing even without the AlmaSEO dashboard. Sitemaps, schema, Evergreen auditing, meta management, and a robots.txt editor give it standalone credibility against Yoast and AIOSEO — then the dashboard connection unlocks AI rewrite, keyword intelligence, and automated publishing that no competitor offers. The Evergreen content auditing system alone (detect aging content, alert, refresh, republish) is a workflow no single competing plugin provides end-to-end.

## Overview

SEO Playground is the on-site SEO toolkit built into the AlmaSEO WordPress Connector Plugin. It adds a full-featured SEO management layer directly inside WordPress — sitemaps, schema markup, content freshness auditing, metadata editing, health scoring, redirects, 404 tracking, and more — without requiring the AlmaSEO dashboard for core functionality.

When connected to the AlmaSEO dashboard, the plugin gains AI-powered optimization: content rewriting, keyword intelligence, content brief generation, FAQ suggestions, and re-optimization alerts for aging posts.

### What It Adds to WordPress

**Admin Menu ("SEO Playground" in the WP sidebar):**

- **Overview** — Connection status and feature summary
- **Connection** — API authentication and dashboard sync
- **Sitemaps** — Multi-tab sitemap management (10+ sitemap types)
- **Evergreen** — Content freshness dashboard with trend charts
- **Post Optimization** — Keyword intelligence sidebar
- **Redirects** — 301/302 redirect manager *(Pro)*
- **404 Logs** — 404 error tracking and redirect conversion *(Pro)*
- **Bulk Metadata** — Mass title/description editor *(Pro)*
- **Robots.txt** — Virtual and physical robots.txt editor

**Post/Page Editor Controls:**

- **SEO Playground meta box** — Tabbed interface with SEO title, meta description, focus keyword, character counters, live Google snippet preview, and optimization suggestions
- **Schema Settings meta box** — Sidebar dropdown for 9 schema types with per-post enable/disable
- **Evergreen Status meta box** — Sidebar badge showing Evergreen/Watch/Stale status with reasons and last-calculated timestamp

**Dashboard Widget:**

- At-a-glance Evergreen content health stats on the WP admin dashboard

---

## Core Features (Standalone — No Dashboard Required)

### Sitemap Engine

Generates 10+ sitemap types automatically:

| Sitemap Type | File Pattern | Details |
|-------------|-------------|---------|
| Post Sitemaps | `/sitemap-posts-*.xml` | Paginated, configurable URLs per file (default 1,000) |
| Page Sitemaps | `/sitemap-pages-*.xml` | Hierarchical page structure |
| Category Sitemaps | `/sitemap-tax-category-*.xml` | Category taxonomy |
| Tag Sitemaps | `/sitemap-tax-tag-*.xml` | Tag taxonomy |
| Custom Post Type | `/sitemap-{cpt}-*.xml` | Auto-detects registered CPTs |
| Custom Taxonomy | `/sitemap-tax-{name}-*.xml` | Auto-detects registered taxonomies |
| Author Sitemaps | `/sitemap-users-*.xml` | Author archive pages |
| Image Sitemaps | Embedded in post sitemaps | Attached images per post |
| Video Sitemaps | `/sitemap-video-*.xml` | YouTube/Vimeo URL detection |
| News Sitemaps | `/sitemap-news.xml` | 48-hour rolling window for Google News |
| Delta/Change Sitemaps | `/sitemap-delta.xml` | Ring buffer of recently changed URLs |
| HTML Sitemaps | `[almaseo_html_sitemap]` shortcode | Human-readable sitemap page |
| Sitemap Index | `/sitemap.xml` | Master file listing all sub-sitemaps |

**Configuration options:** Per-content-type enable/disable, URLs per sitemap limit, static (cached) vs dynamic (on-request) mode, GZIP compression, exclusion rules, priority and frequency customization, news sitemap settings (categories, publisher name, keyword source).

**IndexNow integration:** Instant submission to Bing and Yandex when content changes. API key management, manual/automatic submission toggle, delta tracking for incremental updates.

**Sitemap health monitoring:** Build statistics (duration, file count, URL count), conflict detection with Yoast/AIOSEO/RankMath, hreflang validation (WPML/Polylang), media URL validation.

### Schema / Structured Data

Automatic JSON-LD generation with 9 supported schema types:

- Article, BlogPosting, NewsArticle, WebPage, Product, Review, Recipe, HowTo, FAQPage

**Auto-generated properties:** headline, description, datePublished, dateModified, author (Person), publisher (Organization), url, image (with multi-level fallback: featured image > first content image > site logo > domain placeholder).

**Safety features:**

- **Schema Scrubber** — Detects and removes duplicate JSON-LD from AIOSEO, Yoast, or RankMath to prevent rich result penalties
- **AIOSEO auto-detection** — Automatically disables AlmaSEO schema output when AIOSEO is active
- **Exclusive Schema Mode** — Optional override to take full control of schema output
- **Image fallback chain** — Ensures valid image URLs in every schema block

### Evergreen Content Auditing

Automated content freshness scoring that tracks whether posts are healthy, aging, or stale.

**Status categories:**

- **Evergreen** — Healthy, regularly maintained content
- **Watch** — Content aging, needs attention within 30-90 days
- **Stale** — Outdated, requires immediate refresh (>90 days without update)

**What it analyzes:**

- Content age (days since publication)
- Update frequency (days since last modification)
- Traffic trends (90-day vs previous 90-day clicks/impressions via GSC, when connected)
- Seasonal content detection (regex patterns for holidays, months, year references)
- Explicit dates embedded in content body

**Schedule:**

- Weekly full recalculation via cron (batches of 50 posts to avoid timeouts)
- Daily snapshots for trend tracking
- Manual one-click recalculation per post

**Where results appear:**

- **Evergreen Dashboard** — Overview cards with percentages, trend charts (4/8/12 week rolling averages), sortable at-risk content table, CSV/PDF export
- **Post editor sidebar** — Status badge with reasons and last-calculated timestamp
- **WP Dashboard widget** — At-a-glance stats and at-risk count
- **Email reminders** — Per-post opt-in content refresh notifications via cron

### SEO Health Scoring

Weighted scoring across 15+ signals displayed as a 0-100 gauge in the post editor:

- Title quality (presence, length, keyword inclusion)
- Description quality (presence, length, keyword optimization)
- Content quality (word count, readability, keyword density)
- Focus keyword usage and variations
- Internal link count and quality
- Image optimization (alt text, featured image presence)
- Schema markup validation
- Color-coded status: Red (<50), Yellow (50-79), Green (80+)

### Meta Management

Per-post controls for:

- SEO title with character counter
- Meta description with length indicator
- Focus keyword tracking
- Meta robots (noindex, nofollow, noarchive)
- Canonical URL
- Open Graph tags (title, description, image)
- Twitter Card data

### Metadata Version History

Every meta field change is logged with SHA1 deduplication:

- Full change timeline with user attribution and timestamps
- One-click rollback to any previous version
- Side-by-side diff viewer
- Bulk restore for multiple fields
- Notes system for documenting changes

### Robots.txt Editor

- **Virtual mode** — WordPress filter-based (no file writes needed)
- **Physical mode** — Direct file editing with permission fallback
- Syntax-highlighted editor with live preview
- Recommended defaults with sitemap URL injection

### Redirects Manager *(Pro)*

- Create 301 (permanent) and 302 (temporary) redirects
- Source path normalization and redirect loop detection
- Enable/disable toggles per redirect
- Test redirect URL functionality
- Bulk operations

### 404 Tracker *(Pro)*

- Captures 404 errors via `template_redirect` hook
- Logs: URL, referrer, user agent, IP, timestamp
- Quick-convert any 404 to a redirect
- Filter by date range, search term, referrer
- Ignore list for known non-issues

### Bulk Metadata Editor *(Pro)*

- Mass update titles, descriptions, and canonical URLs
- Filter by post type, status, or category
- Character limit warnings (65 chars title, 160 chars description)
- Reset to defaults option

---

## Dashboard-Connected Features (Require AlmaSEO)

When the plugin is connected to the AlmaSEO dashboard, these AI-powered features become available:

| Feature | What It Does |
|---------|-------------|
| **AI Rewrite** | Generates AI-optimized title and description for any post |
| **Content Brief Generator** | Creates a structured optimization brief for writers |
| **FAQ Generation** | Auto-generates FAQ schema content for a post |
| **Re-Optimization Alerts** | Flags aging posts that need content refresh |
| **Keyword Intelligence** | Intent analysis, difficulty scoring, and keyword suggestions via GSC data |
| **Post Intelligence** | AI-generated content summary and analysis |
| **Automated Publishing** | Dashboard pushes generated articles to WordPress via REST API |

---

## Plugin Compatibility

| Plugin | Behavior |
|--------|----------|
| **Yoast SEO** | Coexists. Sitemap conflict detection; user chooses which plugin manages sitemaps |
| **AIOSEO (Free + Pro)** | Detected automatically. AlmaSEO disables its own schema when AIOSEO is active. Schema Scrubber removes duplicate JSON-LD |
| **Rank Math** | Sitemap conflict detection with user choice. No auto-disable |
| **WPML** | Automatic hreflang tag generation, language-aware sitemaps |
| **Polylang** | Language detection support, compatible with language switching |

---

## System Requirements

| Requirement | Minimum |
|-------------|---------|
| WordPress | 5.6+ (Application Passwords required) |
| PHP | 7.4+ |
| Tested up to | WordPress 6.6 |
| Plugin version | 6.4.8 |
| Multisite | Supported (per-site options, no network-wide settings panel) |

## Why It Matters

Gives every WordPress site a full SEO management layer — sitemaps, schema, meta, content freshness monitoring — that works standalone and gets significantly more powerful when connected to the AlmaSEO dashboard for AI-driven optimization and automated publishing.

## Requirements

- **Integrations:** WordPress API
- **Compatibility:** WordPress 5.6+
- **AI:** OpenAI (via AlmaSEO dashboard, for connected features only)

## Target Audience

Agencies, DIY Business Owners, Freelancers, Solo Practitioners
