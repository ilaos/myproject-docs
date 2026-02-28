# GBP Testimonials in Generated Articles

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    This is a production-time content enhancement (output shaping) rather than a topic-ideation feature. It pairs well with GBP-based intelligence, but its primary value is improving on-page credibility inside the generated article.

## Overview

How it works:
- Fetch up to 50 reviews from the GBP API.
- Filter to 5‑star reviews that contain written text.
- Score reviews for topical relevance (keyword overlap with the article topic).
- Select the top 2 most relevant reviews.
- Insert verbatim quotes only (no paraphrasing or fabrication).
- After successful publish, record which reviews were used.

Usage limits:
- Each review can be used in at most 2 articles.
- When all reviews hit the limit, articles generate normally without testimonials.

Graceful fallback:
- If GBP is not connected, no reviews exist, no qualifying 5‑star text reviews exist, or all reviews are used up, generation proceeds with no errors and no disruption.

Works in both flows:
- Manual post creation (Create a Post form).
- Automated publishing (automation worker).

## Why It Matters

Adds trust signals and social proof using real customer language, without extra manual work, while keeping generation reliable when reviews are unavailable.

## Requirements

- **Integrations:** Google API

