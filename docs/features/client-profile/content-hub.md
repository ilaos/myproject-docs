# Content Hub

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is where AlmaSEO’s “content engine” becomes operational. The Hub turns generation + SEO tooling into a production pipeline: drafts feed scheduled content, scheduled content becomes published posts, and every post has a single detail page that concentrates SEO metadata, exports, quality scoring, and indexing actions. It also bridges both delivery models (WordPress publish vs static export) without splitting the workflow.

## Overview

Child tabs included:
- Drafts: write and manage in-progress articles, then continue editing in the post detail page.
- Scheduled Posts: timeline view of upcoming posts with duplicate-risk indicators and basic schedule controls (edit/cancel stubs).
- Published Posts: searchable, filterable library of published content with status badges and actions (details, export formats, view live, GSC stats, copy URL).

Shared post detail page (/post/<id>):
- Status + generation progress (published/draft/processing/failed).
- Full rendered content preview + SEO metadata (multi-source fallback from Yoast/AIOSEO/AlmaSEO).
- Inline quality score card (Google Cloud NLP) when Content AI is connected.
- Export options (7 formats) and live URL actions when available.

Integrations and delivery modes:
- WordPress (full integration): publish via REST API, upload featured images, read/write Yoast + AIOSEO metadata, store wp_post_id and wp_url.
- Static sites (export-based): no CMS connection required; use exports for Hugo/Jekyll/Next.js, etc.
- Search engine submission: submit URLs to Google Search Console and Bing IndexNow.

## Why It Matters

Gives users one place to create, schedule, publish, and review content for a client, with a consistent post detail workflow that supports exports, CMS publishing, SEO metadata, and indexing submission.

## Requirements

- **Integrations:** Google API, IndexNow, OpenAI API, Wordpress API

## Sub-features

- **[Published Posts](published-posts.md)** *(Pro)* — Content Hub child tab showing the library of published posts for a client.

Dashboard metrics (4 cards):
- Total published count
- Posts this month...
- **[Scheduled Posts](scheduled-posts.md)** *(Pro)* — Content Hub child tab for managing upcoming content in a scheduled timeline view.

UI elements:
- Total scheduled count badge
- Schedule Content bu...
- **[Drafts](drafts.md)** *(Pro)* — Content Hub child tab for managing drafts and in-progress articles.

UI elements:
- Total draft count badge
- Write New Article button
- 3-column c...

