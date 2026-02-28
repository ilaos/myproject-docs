# Wordpress Settings

**Tier:** Core/Free | **Type:** User-Facing UI

!!! tip "Key Insight"
    One tab for everything WordPress: credentials, SEO plugin selection, connection testing, and plugin health diagnostics. The connection badge + error area makes troubleshooting obvious. Auto-test-on-save reduces setup failures. Plugin Health checks prevent silent misconfigurations (wrong plugin selected, plugin inactive, AIOSEO REST API disabled).

## Overview

1) Connection Status (top card): shows WordPress site URL with connection badge (Connected / Error / Unknown), Test Connection button (pings WP REST API), quick-glance details (WP username, SEO plugin, post counts: total/published/drafts), and an error message area.

2) API Configuration (form): WordPress Username, Application Password (show/hide), SEO Plugin dropdown (Yoast, Rank Math, AIOSEO, SEOPress, The SEO Framework, None), step-by-step guide for creating a WP application password, Save WordPress Settings button (saves fields then auto-triggers a connection test), and a Check Plugin Health button (runs diagnostics).

3) Plugin Health Check (expandable results panel): Plugin Detection (confirms selected SEO plugin is installed/active) and REST API Status (AIOSEO-specific check that appears only when AIOSEO is detected; verifies REST API is enabled, requires Pro).

## Why It Matters

Sets up and verifies the WordPress connection so AlmaSEO can publish and manage content on the client’s site reliably.

## Requirements

- **Integrations:** Wordpress API
- **Compatibility:** Wordpress

## Target Audience

Agencies, DIY Business Owners, Freelancers

