---
title: "Structured Data (Schema)"
slug: "structured-data-schema"
type: "feature"
status: "complete"
tier: "Pro"
feature_id: "CA-SCHEMA"
last_updated: "2026-03-04"
---

# Structured Data (Schema)

## Overview

Structured Data is AlmaSEO's umbrella system for generating, validating, detecting, and delivering Schema.org JSON-LD markup across content creation, WordPress publishing, and static site exports.

Rather than being a single tool, Structured Data operates across five interconnected layers: schema is **generated automatically** when content is created, **embedded** when content is exported for static sites, **injected** into WordPress via the Connector plugin, **detected and scored** when sites are analyzed, and **tracked** through a coverage dashboard.

The system supports 10+ primary schema types (Article, FAQPage, HowTo, LocalBusiness, Organization, Service, BreadcrumbList, and more) with 25+ industry-specific LocalBusiness subtypes that map automatically from the site's industry type — so a plumber gets `Plumber` schema, an attorney gets `Attorney` schema, and a dentist gets `Dentist` schema without any manual configuration.

---

## What It Does

### Automatic Schema Generation During Content Creation

When an article is generated through Content Creation, the system automatically analyzes the content and produces the appropriate schema:

| Content Type | Schema Generated |
|-------------|-----------------|
| Blog Article | `Article` or `BlogPosting` with headline, date, author, image, publisher, word count |
| FAQ Page | `FAQPage` with question/answer pairs extracted from content |
| How-To Guide | `HowTo` with numbered steps, total time, estimated cost |
| Service Page | `Service` with provider, area served, price range |
| City/County/State Page | `LocalBusiness` with address, phone, area served, opening hours |

The schema is stored with the post and included in every downstream output — WordPress publishing, static export, and the post detail page.

### Schema Detection & Scoring

When a site is analyzed through the First Impression tool or GEO/AI Search Optimizer, the system scans the page for existing structured data and grades it.

**What it detects:**
- JSON-LD `<script>` blocks
- Microdata (`itemscope`/`itemtype` attributes)
- All standard schema types (Organization, LocalBusiness, FAQPage, HowTo, Article, BreadcrumbList, Service, Review, Product, Person)

**Scoring system (100 points max):**

| Category | Points | What It Checks |
|----------|--------|---------------|
| Basic Identity | 40 | Organization or LocalBusiness present |
| Content Structure | 30 | FAQPage (15), HowTo (10), Article (5) |
| Trust Signals | 20 | Review or AggregateRating data |
| Navigation | 10 | BreadcrumbList present |

**Grades:** A (80+), B (60-79), C (40-59), D (20-39), F (0-19)

The system also generates specific recommendations based on what's missing — prioritized by impact (e.g., missing LocalBusiness for a local business is flagged as CRITICAL).

### Static Export Schema Embedding

When content is exported for static sites (Hugo, Jekyll, Gatsby, Next.js, etc.), schema is automatically embedded in the appropriate format:

| Export Format | How Schema Is Included |
|--------------|----------------------|
| HTML Full | `<script type="application/ld+json">` tags in the `<head>` |
| JSON | `.schema` object with `article`, `faq_page`, `local_business` keys |
| MDX | JSON-LD frontmatter + embedded schema blocks |
| Markdown | JSON-LD in YAML frontmatter (when enabled) |

Schema types included per export are configurable:

| Toggle | Default | What It Controls |
|--------|---------|-----------------|
| `schema_article` | On | Article/BlogPosting schema |
| `schema_faq` | On | FAQPage schema (if FAQ content detected) |
| `schema_local_business` | Off | LocalBusiness schema |

### WordPress Schema Injection

Schema is delivered to WordPress through two mechanisms:

**Via the AlmaSEO Connector Plugin:**
- When content is published to WordPress, schema metadata is pushed alongside SEO fields via the REST API
- Schema type and settings are stored as WordPress post meta fields
- Compatible with AIOSEO, Yoast SEO, and Rank Math

**Via the Gutenberg Schema Panel (SEO Playground):**
- A sidebar panel in the WordPress block editor for per-post schema configuration
- Schema type selector (BlogPosting, Article, custom types)
- Toggle controls: Include Author, Include Featured Image, Include Publisher
- Live validation warnings (missing image, disabled author archives, unconfigured publisher)
- Settings saved as post meta and exposed via WordPress REST API

### Structured Data Dashboard

A coverage tracking dashboard (gated behind `SD_ENABLE=1`) that shows schema status across a site:

**Metrics:**
- Total schema snippets generated
- Valid snippets (passed validation)
- Injected snippets (pushed to WordPress)
- Coverage percentage (posts with schema vs. total posts)

**Snippets table:**
- All post-level schemas with URL, type, status (Valid/Invalid/Injected), date, and JSON viewer

**Bulk actions:**
- Generate schema for all posts
- Refresh coverage data

### Industry-Specific Schema Mapping

The system maps the site's `industry_type` to the most specific Schema.org type automatically:

| Industry | Schema Type |
|----------|------------|
| Legal / Attorney | `Attorney`, `LegalService` |
| Plumbing | `Plumber` |
| HVAC | `HVACBusiness` |
| Electrical | `Electrician` |
| Roofing | `RoofingContractor` |
| General Contracting | `GeneralContractor` |
| Dental | `Dentist` |
| Medical | `Physician`, `MedicalBusiness` |
| Restaurant | `Restaurant`, `FoodEstablishment` |
| Retail | `Store`, `RetailBusiness` |
| Auto Repair | `AutoRepair` |
| Real Estate | `RealEstateAgent` |
| Beauty / Spa | `BeautySalon`, `DaySpa` |
| Fitness | `HealthClub` |
| Accounting / Finance | `AccountingService`, `FinancialService` |
| Insurance | `InsuranceAgency` |
| Cleaning / Landscaping | `HousekeepingService`, `LandscapingOrGardening` |
| Moving / Storage | `MovingCompany`, `SelfStorage` |
| Veterinary / Pets | `VeterinaryCare`, `PetStore` |
| Education | `EducationalOrganization` |
| Hospitality / Travel | `Hotel`, `LodgingBusiness`, `TravelAgency` |
| Professional Services | `ProfessionalService` |

If the industry doesn't match a specific type, it falls back to `LocalBusiness`.

---

## Why It Matters

- **Rich results eligibility** — proper schema markup is what enables FAQ dropdowns, how-to steps, star ratings, and business info cards to appear in Google search results. Without schema, content competes on blue links alone.
- **AI search readiness** — AI-powered search engines (ChatGPT, Perplexity, Claude) use structured data to extract and cite information. Schema makes content machine-readable and increases the chance of being surfaced in AI-generated answers.
- **Zero manual effort** — schema is generated automatically during content creation and embedded automatically during export. Users don't need to learn JSON-LD or manually add markup.
- **Industry-specific accuracy** — a plumber's site gets `Plumber` schema, not generic `LocalBusiness`. This specificity improves relevance signals for search engines.
- **Coverage visibility** — the dashboard shows exactly which posts have schema, which don't, and what types are missing — turning schema from an invisible technical detail into a trackable metric.
- **Trust signal reinforcement** — LocalBusiness schema with accurate NAP data (pulled from the Locations tab) reinforces the same trust signals that NAP Shield monitors, creating consistency between what search engines see in schema and what they find across web citations.

---

## How to Use It

### For Content Creation (Automatic)

No action required. When you generate an article through Content Creation, the appropriate schema is automatically created based on the content type:

1. **Create a Blog Article** → Article/BlogPosting schema generated automatically
2. **Create a FAQ Page** → FAQPage schema with Q&A pairs extracted from content
3. **Create a How-To Guide** → HowTo schema with steps detected from numbered lists
4. **Create a Service Page** → Service schema with provider and area served
5. **Publish to WordPress** → Schema metadata pushed alongside SEO fields

### For Static Site Exports (Automatic)

When exporting content via the Post Details page:

1. Choose any export format (HTML, JSON, MDX, Markdown)
2. Schema is embedded automatically in the appropriate format
3. Deploy the exported file — schema is included and ready for search engines

### For Schema Detection & Analysis

1. Open a site's **Client Profile → Website Analysis → First Impression Tool** or **GEO/AI Search Optimizer**
2. Run an analysis on the site's URL
3. The report includes a **Schema** section showing:
   - Which schema types were detected
   - Schema completeness score (A-F grade)
   - Specific recommendations for missing schema types

### For WordPress Schema Configuration (SEO Playground)

If the SEO Playground plugin is installed:

1. Edit a post in the WordPress block editor
2. Open the **AlmaSEO Schema** panel in the sidebar
3. Select a schema type (BlogPosting, Article, etc.)
4. Toggle author, image, and publisher inclusion
5. Save — schema settings are stored as post meta

### For the Structured Data Dashboard

1. Ensure `SD_ENABLE=1` is set in the environment configuration
2. Access the dashboard via the site's schema management section
3. Review coverage metrics — total, valid, injected, and coverage percentage
4. Use bulk generation to create schema for posts that don't have it yet

### Improving Schema Quality

1. **Fill in Business Information** in Client Profile — business name, phone, email, industry type feed into Organization and LocalBusiness schema
2. **Set up Locations** — address data is required for accurate LocalBusiness schema with PostalAddress
3. **Set the industry type** — enables specific schema type mapping (Plumber, Attorney, Dentist, etc.)
4. **Connect Google Business Profile** — provides hours, ratings, and additional business data for richer schema

---

## Key Settings / Options

### Environment Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| `SD_ENABLE` | `0` | Master flag — enables all structured data routes and dashboard |
| `SD_AUTO_INJECT` | `0` | Enables automatic schema injection to WordPress posts |
| `SD_MAX_FAQ` | `6` | Maximum FAQ items to extract from content |
| `SD_HOWTO_MAX_STEPS` | `15` | Maximum HowTo steps to include |
| `SD_ORG_NAME` | (empty) | Organization name for Article publisher field |
| `SD_ORG_LOGO_URL` | (empty) | Organization logo URL for publisher field |
| `SD_SITE_SEARCH_URL` | (empty) | Search action URL template for WebSite schema |
| `SD_VALIDATE_STRICT` | `0` | Strict validation mode (checks all recommended fields) |
| `SD_TYPES` | `Article,FAQPage,HowTo` | Comma-separated list of enabled schema types |

### Schema Types Reference

| Type | Auto-Generated | Detection | Scoring Weight |
|------|---------------|-----------|---------------|
| Article / BlogPosting | Yes (blog content) | Yes | 5 pts |
| FAQPage | Yes (FAQ content) | Yes | 15 pts |
| HowTo | Yes (how-to content) | Yes | 10 pts |
| LocalBusiness | Yes (location pages) | Yes | 40 pts (identity) |
| Organization | Configurable | Yes | 40 pts (identity) |
| Service | Configurable | Yes | — |
| BreadcrumbList | Configurable | Yes | 10 pts |
| WebSite | Configurable | Yes | — |
| Review / AggregateRating | Detection only | Yes | 20 pts |
| Person | Detection only | Yes | — |

---

## Notes / Edge Cases

- **FAQ extraction is best-effort** — the system parses Q&A patterns from content (headings followed by paragraphs, definition lists). Custom or unusual layouts may not be detected. Maximum 6 FAQ items by default.
- **HowTo detection relies on numbered lists** — flowing prose without numbered steps won't be recognized as HowTo content.
- **LocalBusiness requires location data** — without an address set up in Locations, LocalBusiness schema will be incomplete. The system uses data from the Locations tab, not hardcoded values.
- **WordPress schema injection requires the Connector or Playground plugin** — schema can't be pushed to WordPress without one of these active.
- **Dashboard is behind a feature flag** — `SD_ENABLE=1` must be set in the environment for the dashboard and management routes to be active. Schema generation during content creation works regardless.
- **Schema validation checks required fields** — if strict mode is off (default), only critical fields are checked. Strict mode validates all recommended fields per Schema.org specifications.
- **Multiple schema types can coexist** — a single page can have Article + FAQPage + BreadcrumbList + Organization schema. The system composes them into a single `@graph` structure.

### Sub-features

- **[First Impression Schema Generator](../structured-data/first-impression-schema-generator-manual-tool.md)** — On-demand schema generation tool.
- **[Static Export Schema](../structured-data/static-export-schema-automated-pipeline.md)** — Automated schema embedding in export formats.
- **[Structured Data Dashboard & WordPress Injection](../structured-data/structured-data-dashboard-wordpress-injection.md)** *(Agency)* — Dashboard UI, coverage tracking, and WordPress schema injection.
- **[WordPress Gutenberg Schema Panel](../structured-data/wordpress-gutenberg-schema-panel-editor-integration.md)** — Per-post schema configuration in the WordPress editor.
- **[Schema Detection & Scoring](../structured-data/schema-detection-scoring-background-analysis.md)** — Background analysis of existing schema with A-F grading.
