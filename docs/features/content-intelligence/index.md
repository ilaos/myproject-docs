---
title: "Content Intelligence"
slug: "content-intelligence"
type: "feature"
status: "complete"
tier: "Pro"
feature_id: "CI"
last_updated: "2026-03-04"
---

# Content Intelligence

## Overview

Content Intelligence is AlmaSEO's AI-powered content strategy system. It answers the question **"What should I write next?"** by analyzing a site's existing content, Google Search Console data, Google Business Profile signals, WordPress categories, and live market trends — then generating 8-12 highly-targeted topic recommendations with duplicate risk scoring and one-click article creation.

The system lives inside the **Create Post** form. When a user requests recommendations before writing, Content Intelligence pulls data from every connected source, runs it through GPT-4 Turbo with business-specific context, scores each suggestion against existing content for duplicates, and returns a prioritized list of topics — each tagged with content type, difficulty, topic freshness (evergreen vs. trending), and similarity risk.

It works without any integrations connected. Each additional data source (GSC, GBP, WordPress) makes the recommendations more precise, but the system gracefully degrades when sources are unavailable.

---

## What It Does

### AI Content Recommendations

The flagship capability. One click triggers a full content strategy analysis that typically completes in 45-76 seconds.

**What happens behind the scenes:**

1. **Collects site data** — services offered, business name, industry type, and site URL
2. **Fetches existing content** — all published posts, pages, and their titles from WordPress (REST API) or static site inventory (sitemaps, GSC crawl data)
3. **Runs content analysis:**
   - **Content Hierarchy Check** — compares services offered against existing pages to find missing service pages
   - **Underserved Category Detection** — identifies WordPress categories with fewer than 3 posts
   - **Search Visibility Opportunities** — finds GSC queries with high impressions but low clicks (content that's being found but not clicked)
   - **Live Market Context** — pulls trending keywords and industry news for timely topic suggestions
4. **Builds a GPT-4 Turbo prompt** — injects all collected data, existing titles (to avoid duplicates), underserved categories, GSC opportunities, and market context
5. **Generates 15 topic suggestions** (1.5x buffer)
6. **Runs duplicate detection:**
   - Exact match filtering (title and slug comparison)
   - Semantic similarity scoring (normalized keyword overlap, NLP-based matching)
   - Risk classification: Low (< 0.65), Medium (0.65-0.88), High (>= 0.88, auto-excluded)
7. **Returns 8-12 final recommendations** — each with title, explanation, content type, difficulty, topic type, similarity score, and closest existing match

**Each recommendation includes:**

| Field | Description |
|-------|-------------|
| Title | The suggested topic |
| Explanation | Why this topic matters for the business |
| Content Type | Blog Article, Service Page, FAQ, etc. |
| Difficulty | Low, Medium, or High |
| Topic Type | Evergreen or Trending |
| Similarity Risk | Low (safe), Medium (review), or High (auto-excluded) |
| Closest Match | The most similar existing page, if any |

### Content Hierarchy Warnings

When a site has services listed in its business profile, the system checks whether each service has a dedicated page. Missing service pages are flagged as **Content Hierarchy** warnings — these represent high-priority gaps where a core business offering has no dedicated content.

Users can act on each warning directly: create a service page from the suggestion, save it for later, or dismiss it.

### Underserved Category Detection

For WordPress sites, the system identifies categories with fewer than 3 published posts. These categories are flagged and prioritized in the AI prompt, so the recommendation engine actively suggests topics that would fill those gaps.

### Search Visibility Opportunities

When Google Search Console is connected, the system identifies queries where the site is appearing in search results (high impressions) but not getting clicked (low CTR). These represent content opportunities — the site is already ranking, but the existing content isn't compelling enough to earn the click. The AI factors these into its recommendations.

**Detection criteria:** Impressions > 50 AND Clicks < 10

### Semantic Duplicate Detection

Beyond exact title matching, the system uses NLP-based similarity scoring to catch near-duplicates — topics that cover the same ground with different wording.

**How it works:**

1. Normalizes titles (removes stop words, punctuation, common prefixes)
2. Calculates keyword overlap between suggested and existing content
3. Applies semantic matching with intent adjustment (questions vs. statements score differently)
4. Assigns a risk level:
   - **Low risk** (< 0.65) — safe to write
   - **Medium risk** (0.65-0.88) — shown with a warning, review recommended
   - **High risk** (>= 0.88) — auto-excluded from results

A minimum of 8 recommendations is always returned, even if some carry medium risk.

### Content-Type-Specific Logic

Recommendations are tailored to the content type being created:

| Content Type | Recommendation Focus |
|-------------|---------------------|
| **Blog Articles** | Mix of evergreen and trending topics. Prioritizes underserved categories. Avoids DIY guides and clickbait titles. Injects GSC opportunities and market context. |
| **Service Pages** | Only suggests services directly related to the business's services offered. Focuses on specific variations (e.g., "Ceramic Window Tint" instead of generic "Window Tinting"). |
| **FAQ Pages** | Suggests specific customer questions tied to the business's services. Focuses on decision-making questions, not generic queries. |
| **City/County/State Pages** | Uses service areas and location data to suggest geographic targeting gaps. |

### Click-to-Fill Topic Selection

Users can click any recommendation to automatically populate the topic field in the article creation form. The system fills the correct field based on content type (topic for blogs, service name for service pages, topic area for FAQs). From there, the user can adjust settings and generate the article immediately.

### Data Sources

Content Intelligence pulls from every available source to build the most informed recommendations possible. Each source is optional — the system works without any of them but improves with each one connected.

| Source | What It Provides | Required |
|--------|-----------------|----------|
| **Services Offered** | Filters topics to the business's actual services. Makes recommendations 10x more specific. | Recommended |
| **WordPress Content** | All existing posts and pages via REST API, for gap analysis and duplicate detection | Optional (WordPress sites) |
| **WordPress Categories** | Category post counts for underserved category detection | Optional (WordPress sites) |
| **Google Search Console** | Indexed URLs, top queries, momentum data (rising/declining keywords), search visibility opportunities | Optional |
| **Google Business Profile** | Search queries (what customers search for) and reviews (for topic mining) | Optional |
| **Live Market Context** | Trending keywords and industry news for timely topic suggestions | Automatic |
| **Static Site Inventory** | GSC crawl data, sitemaps, and manual records for non-WordPress sites | Automatic (static sites) |
| **Business Profile** | Business name, industry type, location — used for prompt personalization | Recommended |

### GBP Search Queries

When Google Business Profile is connected, the system fetches the top search keywords that customers use to find the business on Google. These provide direct insight into what potential customers are looking for and can inform topic selection.

### Reviews as Content Mining

GBP reviews (particularly 5-star reviews) can be mined for recurring topics, common questions, and customer language. During article generation, matching reviews are pulled in as testimonials. The review data also surfaces patterns that inform what content would resonate with the audience.

---

## Why It Matters

- **Strategy before writing** — instead of guessing what to write, users get data-backed recommendations informed by their existing content, search performance, and market trends.
- **Prevents duplicate content** — semantic similarity scoring catches near-duplicates before they're created, not after.
- **Fills real gaps** — Content Hierarchy warnings surface missing service pages. Underserved Category detection finds neglected blog categories. Search Visibility opportunities identify queries the site is already ranking for but failing to capture.
- **Adapts to each business** — recommendations are filtered through the business's actual services, industry, and connected data sources. A mold remediation company gets mold topics, not generic marketing advice.
- **One click from strategy to execution** — click a recommendation, adjust settings, generate. No separate planning tool or spreadsheet required.
- **Gets smarter with more data** — works with zero integrations, but each connected source (GSC, GBP, WordPress) adds a layer of precision. Users are rewarded for connecting their services.
- **Saves hours of keyword research** — the combination of GSC data, market trends, and AI analysis replaces manual keyword research, competitor analysis, and content audit workflows.

---

## How to Use It

### Getting Recommendations

1. Navigate to **Create Post** from the sidebar.
2. **Select a site** from the dropdown.
3. **Choose a content type** — Blog Article, Service Page, or FAQ.
4. Click **"Show Recommendations"** — the analysis begins.
5. Wait 45-76 seconds while the system collects data, analyzes gaps, and generates suggestions.
6. Review the **8-12 topic recommendations**, each showing:
   - Topic title and explanation
   - Content type and difficulty badges
   - Evergreen or Trending label
   - Similarity risk indicator (green/yellow/red)
   - Closest existing match (if any)

### Acting on Recommendations

- **Click a topic** to auto-fill the article creation form, then adjust settings and generate.
- **Review Content Hierarchy warnings** — these are high-priority gaps where core services lack dedicated pages. Click "Write" to create the page directly.
- **Check Search Visibility opportunities** — these are queries where the site is already appearing but not getting clicks.
- **Review Technical Priorities** — pages that aren't indexed or are orphaned from the sitemap.

### Improving Recommendation Quality

The more data connected, the better the recommendations:

1. **Fill in Services Offered** in the Client Profile — this is the single biggest improvement.
2. **Connect Google Search Console** — adds search query data, indexing gaps, and momentum signals.
3. **Connect Google Business Profile** — adds customer search queries and review insights.
4. **Publish content regularly** — the system learns from existing content to avoid duplicates and find gaps.

### Refreshing Recommendations

Results are cached for 1 hour per site and content type. Click **Refresh** to force a fresh analysis that bypasses the cache.

---

## Key Settings / Options

### Recommendation Engine

| Setting | Value | Notes |
|---------|-------|-------|
| Recommendations per request | 8-12 | Minimum 8 guaranteed, generated from 15 candidates |
| Cache duration | 1 hour | Per site + content type combination |
| AI model | GPT-4 Turbo | Falls back to GPT-3.5 Turbo on timeout |
| Temperature | 0.7 (first attempt), 0.9 (retry) | Slightly more creative on retry for diversity |
| Max generation attempts | 2 | If first pass yields < 8 good topics, retries with diversity instructions |

### Duplicate Detection Thresholds

| Risk Level | Similarity Score | Behavior |
|------------|-----------------|----------|
| Low | < 0.65 | Shown with green indicator, safe to write |
| Medium | 0.65 - 0.88 | Shown with yellow warning, review recommended |
| High | >= 0.88 | Auto-excluded from results, not clickable |
| Semantic duplicate flag | >= 0.70 | Normalized keyword overlap triggers elevated risk |

### Content Type Prompt Rules

| Content Type | Key AI Instructions |
|-------------|-------------------|
| Blog | Mix evergreen + trending. Prioritize underserved categories. No clickbait numbers, no cliches, no DIY guides. |
| Service | Only suggest services from the business's services_offered list. Focus on specific variations. |
| FAQ | Specific customer questions only. Focus on decision-making questions. Must relate to services offered. |
| City/County/State | Geographic targeting gaps. Format as "[Service] in [City]." |

### Performance

| Metric | Typical | Peak Load |
|--------|---------|-----------|
| Total analysis time | 45-76 seconds | 120+ seconds |
| Frontend timeout | 130 seconds | — |
| Backend timeout | 110 seconds | — |
| OpenAI per-call timeout | 35 seconds | Falls back to GPT-3.5 |

---

## Notes / Edge Cases

- **Not a separate page** — Content Intelligence is embedded in the Create Post form, not a standalone dashboard. Users access it when they're about to create content, exactly when they need strategy guidance.
- **Services Offered is the key input** — without it, recommendations are generic. With it, they're highly specific to the business. This is the single most impactful field to fill in.
- **Graceful degradation** — the system works with zero integrations connected. Each additional source adds precision, but nothing breaks without it.
- **Content Hierarchy is advisory** — the system may flag a service as "missing" when a page exists under a different name. Users can dismiss false positives.
- **GBP integration is read-only** — Content Intelligence only reads GBP data (search queries, reviews). It never writes to or modifies the Google Business Profile.
- **Results are deterministic per cache window** — the same site + content type returns the same results for 1 hour unless the cache is manually busted.
- **Activity logging** — recommendation requests and topic selections are logged for analytics tracking.

### Sub-features

- **[AI Content Recommendations](ai-content-recommendations.md)** *(Pro)* — Full content strategy from one click.
- **[Intelligence Data Sources](intelligence-data-sources.md)** *(Core/Free)* — What feeds the recommendation engine.
- **[Content Authority Engine](content-authority-engine.md)** *(Core/Free)* — Proprietary writing intelligence system that powers all content generation.
