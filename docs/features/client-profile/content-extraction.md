---
title: "Content Extraction"
slug: "content-extraction"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "CP-CONTENT-EXTRACTION"
last_updated: "2026-06-18"
---

# Content Extraction

**Tier:** Core/Free | **Type:** User-Facing UI

!!! tip "Key Insight"
    Rebuilding or redesigning a WordPress site is one of the most common tasks agencies handle — and the most tedious part is gathering all the existing content. Content Extraction pulls everything in one click: posts, pages, custom post types (with ACF fields), media (categorized by role), SEO metadata, site identity (logo, phone, social links), widgets, taxonomies, authors, and menus. It preserves all relationships, tags every image by role, and generates a Content Map that pre-organizes everything into homepage-ready sections (Services, Team, Testimonials, etc.). A developer handed this extraction file can rebuild an entire site without ever visiting the old one.

## Overview

Content Extraction is a tab in the Client Profile sidebar (visible only for WordPress sites) that performs a comprehensive one-click extraction of all site content via the WordPress REST API. Results are stored in AlmaSEO for browsing and can be downloaded as a structured JSON file.

**What gets extracted:**

| Content Type | Data Captured |
|-------------|---------------|
| **Posts** | Full HTML content, title, slug, status, date, excerpt, categories, tags, featured image ID, author, template, content length |
| **Pages** | Same as posts + parent page ID, menu order (preserves page hierarchy) |
| **Custom Post Types** | Auto-detected (attorneys, testimonials, case studies, portfolios, etc.) with full ACF and custom meta fields |
| **Media** | Source URL, alt text, caption, description, MIME type, dimensions, file size, all generated sizes, attached post ID, **role tag** (logo, hero, headshot, background, icon, etc.) |
| **Site Settings** | Site title, tagline, timezone, front page ID, permalink structure, logo URL, favicon URL |
| **Site Identity** | Logo images, favicon, phone numbers, email addresses, social media links, copyright text (scraped from homepage HTML) |
| **Widgets & Sidebars** | All widget areas and their widgets with rendered content (WP 5.8+ block widgets API) |
| **Categories** | Name, slug, description, parent category, post count |
| **Tags** | Name, slug, description, post count |
| **Authors** | Display name, slug, bio/description, website URL, avatar URL |
| **Menus** | Navigation structure via WP 5.9+ block navigation or classic menus (requires REST API exposure) |
| **SEO Metadata** | SEO title, meta description, focus keyword, canonical URL, OG title/description/image, schema JSON |
| **Content Map** | All content pre-organized into homepage-ready sections (About, Services, Team, Testimonials, Contact, FAQ, Blog, Portfolio, Pricing, Careers) with snippets |

**Relationship maps included:**

- Post → featured image (with URL and alt text)
- Page → featured image
- Page → parent page (full hierarchy tree)
- Media → attached post/page
- Category/tag ID → name lookup
- Author ID → name lookup

## How It Works

1. Navigate to any WordPress site in your Client Profile.
2. Click **Content Extraction** in the sidebar.
3. Click **Extract Content** — the extraction runs in the background.
4. A progress bar shows each step: Posts → Pages → Categories → Tags → Media → Authors → Menus → Site Settings → Custom Content Types → Widgets & Sidebars → Site Identity → Image Categorization → SEO Metadata → Content Map.
5. When complete, results appear in a tabbed interface with stats cards, an extraction report, and a content map.
6. Download the full extraction as a structured JSON file at any time.

Typical extraction time: **15–45 seconds** depending on the amount of content and whether the SEO scrape fallback is needed.

## Custom Post Types & Custom Fields

Many WordPress sites use custom post types (CPTs) for structured content — attorneys at a law firm, properties on a real estate site, menu items at a restaurant. These are invisible if you only extract posts and pages.

Content Extraction automatically:

1. Queries `/wp-json/wp/v2/types` to discover all registered CPTs
2. Skips WordPress built-in types (revisions, blocks, CSS, etc.)
3. Fetches all items for each custom type with full content
4. Includes **ACF fields** (`acf` object) and **custom meta** (`meta` object) on every item

This means structured data like an attorney's phone number, a testimonial's star rating, or a case study's outcome is captured as data — not buried in an HTML blob.

!!! info "ACF Plugin Required"
    Advanced Custom Fields data is only available via the REST API if the ACF plugin is installed and has REST API support enabled (default in ACF 5.11+). Other custom field plugins (Pods, Meta Box, JetEngine) that register their fields with the REST API are also supported.

## Site Settings & Identity

### Site Settings (REST API)

Extracted from `/wp-json/wp/v2/settings` and the public REST API index:

- Site title and tagline
- Site URL
- Timezone and date/time formats
- Front page configuration (static page vs latest posts, front page ID, blog page ID)
- Custom logo and site icon (favicon) — resolved to actual image URLs

!!! note "Admin permissions"
    The settings endpoint may require administrator-level authentication. If the authenticated user doesn't have access, basic site info (title, tagline) is retrieved from the public REST API index as a fallback.

### Site Identity (Homepage Scrape)

Elements that live in theme settings, widgets, or hardcoded templates aren't available via the REST API. To capture these, the extractor scrapes the live homepage HTML and extracts:

- **Logo images** — detected by CSS class (`custom-logo`, `site-logo`, `header-logo`), alt text containing "logo", and filenames containing "logo"
- **Favicon** — from `<link rel="icon">` and `<link rel="apple-touch-icon">` tags
- **Phone numbers** — from `tel:` links and visible patterns matching common phone formats
- **Email addresses** — from `mailto:` links
- **Social media links** — Facebook, Twitter/X, Instagram, LinkedIn, YouTube, TikTok, Pinterest, Yelp, GitHub
- **Copyright text** — from footer content matching `©` or `copyright` patterns

## Widgets & Sidebars

Extracted via the WordPress 5.8+ block widgets REST API (`/wp-json/wp/v2/sidebars` and `/wp-json/wp/v2/widgets`):

- All registered sidebar/widget areas with names and descriptions
- Individual widgets with their type, sidebar assignment, and rendered HTML content
- Widget instance data (settings/configuration)

This captures header contact info, footer CTAs, sidebar elements, and any other widget-based content that doesn't live in posts or pages.

## Image Role Tagging

Every media item is automatically categorized by its likely role:

| Role | How It's Detected |
|------|-------------------|
| **logo** | Filename contains "logo" or "brand", matched to site logo URL, or found via homepage scrape |
| **favicon** | Filename contains "favicon" or "site-icon", matched to site icon URL |
| **hero** | Filename contains "hero", "banner", "slider", "carousel", or image has very wide aspect ratio (3:1+) at 1200px+ wide |
| **headshot** | Filename or alt text contains "headshot", "portrait", "team", "staff", "attorney", "profile" |
| **background** | Filename contains "background", "bg-", "pattern", "texture", "overlay" |
| **icon** | Filename contains "icon", "glyph", "symbol" and image is under 200px wide |
| **featured_image** | Used as a featured image on a post or page (not matched by other rules) |
| **document** | Non-image media (PDFs, documents, etc.) |
| **content** | Default — general content images |

Each media item has a `role` field in the JSON. Role counts are shown in the extraction stats and report.

## Content Map

The Content Map is the intelligence layer that transforms raw extracted content into an actionable reference for site rebuilds. It pre-organizes all posts, pages, and custom post type items into homepage-ready sections.

**Sections detected:**

| Section | Content Matched By |
|---------|-------------------|
| **About** | Slugs/titles containing "about", "who-we-are", "our-story", "our-firm" |
| **Services** | "service", "practice", "what-we-do", "areas-of-practice", "expertise" |
| **Team** | "team", "attorney", "lawyer", "staff", "people" |
| **Testimonials** | "testimonial", "review", "client-stories", "success-stories", "case-results" |
| **Contact** | "contact", "get-in-touch", "reach-us", "location", "office" |
| **FAQ** | "faq", "frequently-asked", "questions", "help" |
| **Blog** | All posts default to blog; also "news", "articles", "insights", "resources" |
| **Portfolio** | "portfolio", "projects", "work", "gallery", "case-study" |
| **Pricing** | "pricing", "rates", "packages", "plans", "fees" |
| **Careers** | "career", "jobs", "hiring", "join-us", "employment" |

**Each item in the content map includes:**

- Title and slug
- A **text snippet** (first 200 characters of clean content) — ready to paste into a homepage section
- **SEO description** (if available) — often an even better snippet since it's already written to be concise
- Featured image reference (URL and alt text)
- Word count
- Content type badge (Post, Page, or CPT name)
- Custom fields (for CPT items with ACF data)
- Publication status

**Homepage detection:** If the site uses a static front page, the Content Map identifies it by ID and shows its SEO description.

Posts are also categorized by their WordPress categories — if a post is in a "Testimonials" category, it's grouped under Testimonials rather than Blog.

## SEO Metadata Extraction

Content Extraction captures SEO metadata from the site's SEO plugin. It supports:

| Plugin | Method | Fields Captured |
|--------|--------|----------------|
| **Yoast SEO** | REST API (`yoast_head_json`) | Title, description, canonical, OG title/description/image, schema JSON |
| **RankMath** | REST API (`rank_math_*` meta) | Title, description, focus keyword, canonical, robots |
| **AIOSEO** | REST API (`aioseo` object or meta) | Title, description, focus keyword, canonical, OG title/description |
| **SEOPress** | REST API (`_seopress_*` meta) | Title, description, canonical, OG title/description |
| **The SEO Framework** | REST API (`_genesis_*` meta) | Title, description |

### HTML Scrape Fallback

When the SEO plugin doesn't expose its data to the WordPress REST API (common with AIOSEO), the extractor automatically falls back to **scraping the live page HTML** for each published page. It extracts:

- `<title>` tag
- `<meta name="description">` tag
- `<link rel="canonical">` tag
- `<meta property="og:title">`, `og:description`, `og:image` tags

This fallback is capped at 50 pages to avoid excessive requests. Drafts and private pages are skipped (they have no public URL to scrape).

In the results, SEO data from the fallback is marked with `seo_plugin: "html_scrape"` so you know the source.

SEO metadata is also extracted for custom post type items, not just posts and pages.

!!! info "Why some pages have no SEO data"
    Pages with no SEO metadata are typically drafts (no public URL to scrape) or pages where the SEO plugin has no custom title/description set. The extraction report explains the specific count and reason.

## Page Builder Markup Cleanup

Many WordPress sites use page builders (Elementor, Divi, WPBakery) that wrap content in dozens of nested `<div>` elements with builder-specific classes and data attributes. This markup is useless during a migration — you need the actual content.

Content Extraction automatically strips builder wrapper markup while preserving the real content (headings, text, images, links, lists). Each post, page, and CPT item includes:

- `content` — the original HTML exactly as WordPress stores it
- `content_clean` — the cleaned version with builder markup removed

The cleanup handles:

- **Elementor:** `elementor-section`, `elementor-column`, `elementor-widget-wrap`, `elementor-element`, data attributes
- **Divi:** `et_pb_section`, `et_pb_row`, `et_pb_column`, `et_pb_text_inner`
- **WPBakery:** `vc_row`, `vc_column`, `wpb_wrapper`, `wpb_text_column`
- **BSF markers:** `bsf_rt_marker` divs

## Extraction Report

Every extraction generates an automated report explaining what was captured and what wasn't. The report appears as a collapsible panel in the dashboard and is included in the JSON download.

**Report sections:**

- **Summary** (green checks): What was successfully extracted with counts — e.g., "23 posts extracted with full HTML content, excerpts, and taxonomy assignments." Also covers site settings, custom post types found, widgets captured, site identity data, image role breakdown, and content map sections.
- **Warnings** (yellow triangles): What's missing and why — e.g., menus not available via REST API, missing alt text count, SEO plugin not exposing data, settings endpoint requiring admin auth.
- **Notes** (blue info): Additional context — e.g., page builder markup detected and cleaned, low-resolution images flagged, HTML scrape fallback details, image role categorization summary.

Example report entries:

> "Site settings extracted: 'Smith & Associates Law Firm' — 'Experienced Legal Representation'. Static front page (ID: 42). Custom logo found. Favicon found."

> "Custom post types found: Attorneys (6), Testimonials (12), Practice Areas (8). These contain structured content with any ACF/custom fields included."

> "Site identity extracted from homepage HTML: 2 logo image(s), phone: (404) 555-1234, email: info@example.com, 4 social media link(s), copyright text."

> "Media items categorized by role: 2 logo, 1 favicon, 4 hero, 6 headshot, 3 background, 12 featured_image. Remaining 240 classified as general content images."

> "Content map generated with 8 sections: about (3), blog (23), contact (2), faq (1), services (8), team (6), testimonials (12), uncategorized (10)."

## Content Preview

Clicking the eye icon on any post or page opens a preview modal with three view modes:

| View | What It Shows |
|------|---------------|
| **Rendered** | The cleaned HTML rendered as a web page (builder markup stripped) |
| **Clean HTML** | Plain text only — all HTML tags removed, ready to paste into any editor |
| **Source** | The raw original HTML source code (for developers) |

If SEO metadata exists for the item, it appears in a banner above the content showing the SEO plugin, title (with character count), description (with character count), focus keyword, canonical URL, and OG data.

A **Copy** button copies the currently displayed content to the clipboard.

## JSON Download Format

The downloadable JSON file contains all extracted data in a single structured file:

```json
{
  "extraction_id": 5,
  "site_id": 6,
  "site_name": "My_Website",
  "extracted_at": "2026-06-18T02:30:00.000000",
  "stats": {
    "posts": 23,
    "pages": 65,
    "categories": 22,
    "tags": 21,
    "media": 268,
    "authors": 1,
    "menus": 0,
    "custom_post_types": 26,
    "site_settings": 1,
    "site_identity": 1,
    "widgets": 8,
    "_elapsed_sec": 35.2,
    "_total_items": 400,
    "_seo_metadata_found": 75,
    "_seo_from_api": 0,
    "_seo_from_scrape": 75,
    "_image_roles": {"logo": 2, "hero": 4, "headshot": 6, "content": 240, ...},
    "_content_sections": 8
  },
  "posts": [...],
  "pages": [...],
  "categories": [...],
  "tags": [...],
  "media": [...],
  "authors": [...],
  "menus": [...],
  "site_settings": {
    "site_title": "Smith & Associates",
    "tagline": "Experienced Legal Representation",
    "page_on_front": 42,
    "site_logo_url": "https://example.com/wp-content/uploads/logo.png",
    "site_icon_url": "https://example.com/wp-content/uploads/favicon.png",
    ...
  },
  "site_identity": {
    "logo_urls": ["https://example.com/.../logo.png"],
    "phone_numbers": ["(404) 555-1234"],
    "email_addresses": ["info@example.com"],
    "social_links": ["https://facebook.com/...", "https://linkedin.com/..."],
    "copyright_text": "© 2026 Smith & Associates. All rights reserved.",
    "favicon_url": "https://example.com/.../favicon.ico"
  },
  "custom_post_types": {
    "attorney": {
      "name": "Attorneys",
      "rest_base": "attorney",
      "count": 6,
      "items": [
        {
          "id": 101,
          "title": "John Smith",
          "content_clean": "...",
          "acf": {"phone": "555-1234", "position": "Managing Partner", ...},
          "seo": {...}
        }
      ]
    }
  },
  "widgets": {
    "sidebars": [...],
    "widgets": [...]
  },
  "relationships": {
    "post_featured_images": {},
    "page_featured_images": {},
    "media_used_by": {},
    "page_hierarchy": {},
    "category_map": {},
    "tag_map": {},
    "author_map": {}
  },
  "content_map": {
    "homepage": {"id": 42, "title": "Home", "seo": {...}},
    "sections": {
      "services": [{"title": "Family Law", "snippet": "Our family law team...", ...}],
      "team": [{"title": "John Smith", "snippet": "Managing Partner...", "custom_fields": {...}}],
      "testimonials": [{"title": "Client Review", "snippet": "Smith & Associates helped...", ...}]
    },
    "section_summary": {"services": 8, "team": 6, "testimonials": 12, ...}
  },
  "report": {
    "summary": [...],
    "warnings": [...],
    "notes": [...]
  }
}
```

## Dashboard UI

The extraction results are displayed in a tabbed interface:

| Tab | Contents |
|-----|----------|
| **Posts** | Table with title, status badge, date, categories, word count, SEO indicator (green/red search icon), author name, preview button |
| **Pages** | Table with title, status badge, slug, parent page, word count, SEO indicator, preview button |
| **Media** | Grid of thumbnails with title, dimensions, file size, alt text status (green check or yellow warning), role tag |
| **Taxonomies** | Side-by-side view: categories as a list with post counts, tags as badges with counts |
| **Menus** | Menu items with titles and URLs (or "not available" message with explanation) |
| **Site Info** | Four cards: Site Settings (title, tagline, logo, favicon), Site Identity (phone, email, social links, copyright), Widgets & Sidebars (areas and widget previews), Custom Post Types (CPT names with item counts and ACF indicators) |
| **Content Map** | Accordion organized by section type (Services, Team, Testimonials, etc.) with tables showing title, snippet, content type, word count, featured image, and custom field indicators. Homepage identification at the top. |

Stats cards across the top show counts for: Posts, Pages, Custom Types (if any), Media, Categories, Tags, Authors, SEO Meta (X/Y format), and Content Map Sections.

## Past Extractions

All extractions are saved in the database and listed in the Content Extraction tab. Each entry shows:

- Status badge (Completed / Partial / Failed)
- Total items extracted
- Elapsed time
- Breakdown (posts, pages, media counts)
- Date/time

You can view any past extraction, download its JSON, or delete it. Multiple extractions over time can be used to track content changes on a site.

## Requirements

- **Site type:** WordPress only (not available for static or project sites)
- **Connection:** Valid WordPress REST API credentials (username + application password or JWT token) stored in site settings
- **Authentication:** The WordPress user must have sufficient permissions to read posts, pages, media, categories, tags, users, settings, widgets, and custom post types via the REST API. Administrator-level access provides the most complete extraction.
- **Integrations:** WordPress REST API. Optional: Advanced Custom Fields plugin for structured field extraction. Optional: WP REST API Menus plugin for classic menu extraction.

## Limitations

- **Media files are not downloaded** — only metadata and URLs are captured. The actual image files remain on the WordPress server.
- **Navigation menus** require either WordPress 5.9+ block-based navigation or the "WP REST API Menus" plugin to be exposed via the API. Most classic theme menus are not available.
- **SEO metadata availability** depends on the SEO plugin. Yoast and RankMath expose data to the REST API by default. AIOSEO and others may not, triggering the HTML scrape fallback (which captures titles and descriptions but not plugin-specific data like focus keywords or schema markup).
- **HTML scrape fallback** only works for published content with public URLs. Drafts and private pages are skipped.
- **Builder markup cleanup** handles Elementor, Divi, and WPBakery. Other builders (Beaver Builder, Oxygen, Bricks) may leave some wrapper markup in the cleaned content.
- **Extraction is capped** at 2,000 items per content type and 50 pages for the SEO scrape fallback.
- **Widget extraction** requires WordPress 5.8+ with the block widgets API. Older WordPress installations or sites using classic widgets may not return widget data.
- **Site settings** endpoint may require administrator authentication. When unavailable, basic info (title, tagline) is retrieved from the public REST API index.
- **ACF fields** require the ACF plugin to register fields with the REST API (default in ACF 5.11+).
- **Image role tagging** uses heuristics (filename patterns, dimensions, context). Unusual naming conventions may result in incorrect categorization.
- **Content Map section detection** is pattern-based. Content with non-standard slugs or titles may be categorized as "uncategorized."

## Technical Details

**Backend files:**

- `utils/wp_content_extractor.py` — extraction engine with paginated fetching, SEO extraction, builder markup cleanup, HTML scrape fallback, site settings, CPT detection, widget extraction, homepage identity scraping, image role tagging, content map generation, and report generation
- `dashboard.py` — 6 API routes (`/api/content-extraction/*`)

**API routes:**

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | `/api/content-extraction/start` | Start a new extraction |
| GET | `/api/content-extraction/status/<id>` | Poll extraction progress |
| GET | `/api/content-extraction/<id>` | Get full extraction results |
| GET | `/api/content-extraction/<id>/download` | Download as JSON file |
| GET | `/api/content-extractions?site_id=X` | List past extractions |
| DELETE | `/api/content-extraction/<id>` | Delete an extraction |

**WordPress REST API endpoints used:**

| Endpoint | Purpose |
|----------|---------|
| `/wp-json/wp/v2/posts` | Posts with meta/ACF |
| `/wp-json/wp/v2/pages` | Pages with meta/ACF |
| `/wp-json/wp/v2/categories` | Categories |
| `/wp-json/wp/v2/tags` | Tags |
| `/wp-json/wp/v2/media` | Media library |
| `/wp-json/wp/v2/users` | Authors |
| `/wp-json/wp/v2/navigation` | Block-based menus (WP 5.9+) |
| `/wp-json/wp-api-menus/v2/menus` | Classic menus (plugin required) |
| `/wp-json/wp/v2/settings` | Site settings (admin required) |
| `/wp-json/wp/v2/types` | Registered post types (for CPT discovery) |
| `/wp-json/wp/v2/{cpt_rest_base}` | Custom post type content |
| `/wp-json/wp/v2/sidebars` | Widget areas (WP 5.8+) |
| `/wp-json/wp/v2/widgets` | Individual widgets (WP 5.8+) |
| `/wp-json/` | Public site index (fallback for title/tagline) |
| Site homepage (HTML) | Identity scraping (logo, phone, social, copyright) |
| Individual page URLs (HTML) | SEO metadata fallback scraping |

**Database:** `content_extractions` table (auto-created on first use, no migration needed)

**Execution model:** Runs in a background thread with progress updates written to the database via raw sqlite3 (bypasses Flask's request context). The frontend polls `/status` every 2 seconds during extraction.
