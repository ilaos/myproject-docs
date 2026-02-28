# WordPress Gutenberg Schema Panel (Editor Integration)

**Tier:** Pro | **Type:** Integration

!!! tip "Key Insight"
    This is schema control where WordPress users already work. It reduces round-trips and makes schema configuration feel native to publishing.

## Overview

WordPress editor (Gutenberg sidebar) integration in the AlmaSEO SEO Playground plugin that lets users configure schema settings per post and inject schema on save/publish.

User surface:
- Gutenberg sidebar panel.
- Classic Editor variant exists (schema-meta-tab.js).

Generation & delivery:
- User sets toggles; saved as post meta (_almaseo_schema_type, _almaseo_schema_include_author, etc.).
- Schema rendered server-side using meta values.
- Injected into the WP post on save/publish.
- Validates and warns about missing data (featured image, author archives, publisher).

Schema types:
- BlogPosting (default)
- Article

Primary inputs:
- WP post data (title/content/featured image)
- User-configured post meta
- Author + publisher configuration

## Why It Matters

Lets WordPress users control schema per post directly in the editor, with validation to prevent missing requirements for rich results.

## Requirements

- **Integrations:** Wordpress API
- **Compatibility:** Wordpress

## Target Audience

Agencies, Freelancers

