# Published Posts

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Published Posts is the “distribution + validation” surface. It connects publishing outputs (WP URL, exports) to feedback loops (GSC stats, submission status), and keeps operational content work from getting lost across tools.

## Overview

Dashboard metrics (4 cards):
- Total published count
- Posts this month
- Average word count
- GSC submission rate (%)

Controls:
- Search by title
- Filters: All Posts, Submitted to GSC, Not in GSC, Last 7 days, Last 30 days
- Sort: Newest/Oldest, Most/Least Words, Alphabetical
- New Article button

Post cards show:
- Title (links to post detail page)
- Time-elapsed badge (Today, X days/weeks/months ago)
- Word count + estimated read time
- GSC submitted badge (if applicable)
- Featured image badge (if applicable)
- Publication date and categories

Actions per post:
- Details (open post detail page)
- Export dropdown (7 formats): Markdown, HTML Full Page, HTML Body Only, JSON (Headless CMS), MDX (React), Structured JSON, Structured YAML, Featured Image download
- View Live (WordPress URL; WP sites only)
- GSC Stats (link to Search Console performance for that URL)
- Copy URL

Pagination: 10 posts/page with client-side search/filter/sort.

## Why It Matters

Makes it easy to find and reuse published content, export it in multiple formats, and quickly jump to live URLs or Search Console stats for performance validation.

## Requirements

- **Integrations:** Google API, IndexNow, Wordpress API

