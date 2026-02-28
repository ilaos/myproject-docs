# AlmaSEO WordPress Connector Plugin

**Tier:** Pro | **Type:** Integration

!!! tip "Key Insight"
    Treat this as the foundation of the WordPress integration story: install + connect + verify + capability-detect. It unlocks every other WordPress-dependent feature and should be the first dependency for editor panels, metadata syncing, and publishing.

## Overview

Core capabilities:
1) Secure authentication: generates/manages WordPress Application Passwords for API access; supports auto-connect via a shared secret; stale password detection clears orphaned credentials.
2) SEO metadata management: writes title, description, keywords, Open Graph, Twitter cards, canonical URLs, robots directives via REST API; compatible with AIOSEO (Free + Pro), Yoast SEO, and Rank Math.
3) Site capabilities reporting: endpoint exposes post types, taxonomies, REST endpoints, and whether Application Passwords/custom fields are enabled.
4) Connection verification: endpoint confirms plugin is active, checks plugin version, and returns site info (name, URL, WordPress version).
5) SEO Playground: meta box in post/page editor for SEO Title, Meta Description, Focus Keyword, Schema Type, and SEO Notes; character counters and live Google snippet preview.
6) AI-powered features (when connected): Post Intelligence (AI content summary), Keyword Intelligence (intent/difficulty), and Re-Optimization Alerts for aging posts.
7) SEO status detection: reports which SEO plugin is installed, version, Pro/free, and capabilities so AlmaSEO can write metadata correctly.
8) Security: CORS restricted to http://api.almaseo.com; secret-based endpoint protection; nonce verification; admin-only permission checks; timing-safe secret comparison (hash_equals).

## Why It Matters

Lets users securely connect WordPress to AlmaSEO so AlmaSEO can publish content, manage SEO metadata, and run optimization workflows without manual copy/paste.

## Requirements

- **Integrations:** Wordpress API
- **Compatibility:** Wordpress

