# Static Export Schema (Automated Pipeline)

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    Bridges the gap for non-WordPress users: AlmaSEO exports aren’t just content, they’re SEO-ready packages. Auto-including LocalBusiness schema is a strong local SEO differentiator.

## Overview

User surface:
- No dedicated screen; schema is included inside exported files from Post Details.
- Users see it when opening the downloaded HTML/JSON/YAML.

Generation & delivery:
- Auto-generated during export (no button/settings).
- Backend SchemaGenerator in backend/exporters/ is called by exporters.
- Embedded into outputs:
	- HTML Full Page: <script type="application/ld+json"> in <head>
	- HTML Body: appended after </article> with guidance to move to <head>
	- JSON export: included as a field
	- Legacy WP export: included in YAML/JSON
- Not stored separately; lives inside structured_content JSON on the post.

Schema types:
- Article (always)
- FAQPage (if FAQ sections exist)
- LocalBusiness (industry mapping + aggregateRating + phone formatting)
- BreadcrumbList
- Service

Primary inputs:
- Structured content model (title, sections, slug, etc.)
- get_business_info_with_location(site_id)
- GBP rating data (from reviews cache, injected into business_info)
- Industry, featured image, service area / nearby cities, page type

## Why It Matters

Ensures exports ship with ready-to-use schema markup, improving SEO for static sites and non-WordPress workflows without extra manual steps.

## Target Audience

Agencies, DIY Business Owners, Freelancers

