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
    Rebuilding or redesigning a WordPress site is one of the most common tasks agencies handle — and the most tedious part is gathering all the existing content. Content Extraction pulls everything in one click: posts, pages, media, SEO metadata, taxonomies, authors, and menus. It preserves the relationships between content (which image belongs to which post, which page is a child of which parent) and generates a report explaining what was captured and what couldn't be extracted.

## Overview

Content Extraction is a tab in the Client Profile sidebar (visible only for WordPress sites) that performs a one-click extraction of all site content via the WordPress REST API. Results are stored in AlmaSEO for browsing and can be downloaded as a structured JSON file.

**What gets extracted:**

| Content Type | Data Captured |
|-------------|---------------|
| **Posts** | Full HTML content, title, slug, status, date, excerpt, categories, tags, featured image ID, author, template, content length |
| **Pages** | Same as posts + parent page ID, menu order (preserves page hierarchy) |
| **Media** | Source URL, alt text, caption, description, MIME type, dimensions, file size, all generated sizes (thumbnail through full), attached post ID |
| **Categories** | Name, slug, description, parent category, post count |
| **Tags** | Name, slug, description, post count |
| **Authors** | Display name, slug, bio/description, website URL, avatar URL |
| **Menus** | Navigation structure via WP 5.9+ block navigation or classic menus (requires REST API exposure) |
| **SEO Metadata** | SEO title, meta description, focus keyword, canonical URL, OG title/description/image, schema JSON |

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
4. A progress bar shows each step: Posts → Pages → Categories → Tags → Media → Authors → Menus → SEO Metadata.
5. When complete, results appear in a tabbed interface with stats cards and an extraction report.
6. Download the full extraction as a structured JSON file at any time.

Typical extraction time: **10–30 seconds** depending on the amount of content (a site with 65 pages and 268 media items completes in under 30 seconds).

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

!!! info "Why some pages have no SEO data"
    Pages with no SEO metadata are typically drafts (no public URL to scrape) or pages where the SEO plugin has no custom title/description set. The extraction report explains the specific count and reason.

## Page Builder Markup Cleanup

Many WordPress sites use page builders (Elementor, Divi, WPBakery) that wrap content in dozens of nested `<div>` elements with builder-specific classes and data attributes. This markup is useless during a migration — you need the actual content.

Content Extraction automatically strips builder wrapper markup while preserving the real content (headings, text, images, links, lists). Each post and page includes:

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

- **Summary** (green checks): What was successfully extracted with counts — e.g., "23 posts extracted with full HTML content, excerpts, and taxonomy assignments."
- **Warnings** (yellow triangles): What's missing and why — e.g., menus not available via REST API, missing alt text count, SEO plugin not exposing data.
- **Notes** (blue info): Additional context — e.g., page builder markup detected and cleaned, low-resolution images flagged, HTML scrape fallback details.

Example warnings the report might show:

> "Navigation menus could not be extracted. WordPress does not expose menus via the REST API by default."

> "42 of 268 media items are missing alt text. This should be addressed during the rebuild for accessibility and SEO."

> "No SEO plugin data was available via the REST API. All SEO metadata was recovered by scraping the live page HTML."

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
  "extracted_at": "2026-06-18T01:22:45.123456",
  "stats": {
    "posts": 23,
    "pages": 65,
    "categories": 22,
    "tags": 21,
    "media": 268,
    "authors": 1,
    "menus": 0,
    "_elapsed_sec": 27.4,
    "_total_items": 400,
    "_seo_metadata_found": 50,
    "_seo_from_api": 0,
    "_seo_from_scrape": 50
  },
  "posts": [...],
  "pages": [...],
  "categories": [...],
  "tags": [...],
  "media": [...],
  "authors": [...],
  "menus": [...],
  "relationships": {
    "post_featured_images": {},
    "page_featured_images": {},
    "media_used_by": {},
    "page_hierarchy": {},
    "category_map": {},
    "tag_map": {},
    "author_map": {}
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
| **Media** | Grid of thumbnails with title, dimensions, file size, alt text status (green check or yellow warning) |
| **Taxonomies** | Side-by-side view: categories as a list with post counts, tags as badges with counts |
| **Menus** | Menu items with titles and URLs (or "not available" message with explanation) |

Stats cards across the top show counts for: Posts, Pages, Media, Categories, Tags, Authors, and SEO Meta (X/Y format showing coverage).

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
- **Authentication:** The WordPress user must have sufficient permissions to read posts, pages, media, categories, tags, and users via the REST API
- **Integrations:** WordPress REST API (no additional plugins required, though SEO plugins that expose data to the REST API provide richer metadata)

## Limitations

- **Media files are not downloaded** — only metadata and URLs are captured. The actual image files remain on the WordPress server.
- **Navigation menus** require either WordPress 5.9+ block-based navigation or the "WP REST API Menus" plugin to be exposed via the API. Most classic theme menus are not available.
- **SEO metadata availability** depends on the SEO plugin. Yoast and RankMath expose data to the REST API by default. AIOSEO and others may not, triggering the HTML scrape fallback (which captures titles and descriptions but not plugin-specific data like focus keywords or schema markup).
- **HTML scrape fallback** only works for published content with public URLs. Drafts and private pages are skipped.
- **Builder markup cleanup** handles Elementor, Divi, and WPBakery. Other builders (Beaver Builder, Oxygen, Bricks) may leave some wrapper markup in the cleaned content.
- **Extraction is capped** at 2,000 items per content type and 50 pages for the SEO scrape fallback.

## Technical Details

**Backend files:**

- `utils/wp_content_extractor.py` — extraction engine with paginated fetching, SEO extraction, builder markup cleanup, HTML scrape fallback, and report generation
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

**Database:** `content_extractions` table (auto-created on first use, no migration needed)

**Execution model:** Runs in a background thread with progress updates written to the database via raw sqlite3 (bypasses Flask's request context). The frontend polls `/status` every 2 seconds during extraction.
