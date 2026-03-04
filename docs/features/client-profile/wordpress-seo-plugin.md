---
title: "WordPress SEO Plugin"
slug: "wordpress-seo-plugin"
type: "feature"
status: "draft"
last_updated: "2026-03-04"
---

# WordPress SEO Plugin

## Overview

A Client Profile tab that shows which SEO plugin is installed on the connected WordPress site, detected automatically from the site's connection data.

## What It Does

When a WordPress site is connected to AlmaSEO, this tab automatically detects the active SEO plugin and displays it. It also provides a dropdown to manually select or override the detected plugin.

Supported SEO plugins include:

- AlmaSEO SEO Playground
- Yoast SEO
- Rank Math
- All in One SEO (AIOSEO)
- Other common SEO plugins

The detected plugin determines how AlmaSEO writes SEO metadata (title, description, keywords, Open Graph, etc.) to the WordPress site, since each plugin stores metadata differently.

## Why It Matters

- **Automatic detection** — no manual configuration needed; AlmaSEO figures out which SEO plugin is active.
- **Correct metadata delivery** — ensures titles, descriptions, and schema are written to the fields the active SEO plugin actually reads.
- **Plugin flexibility** — supports switching SEO plugins without breaking the AlmaSEO integration.

## How to Use It

1. Open a site's **Client Profile**.
2. Navigate to the **WordPress SEO Plugin** tab.
3. The detected SEO plugin is displayed automatically.
4. To override, use the dropdown to select a different plugin.

## Notes / Edge Cases

- Detection relies on data returned by the AlmaSEO WordPress Connector Plugin during connection.
- If no SEO plugin is detected, AlmaSEO defaults to writing metadata via its own fields.
- Changing the selection affects how all future content publishes write SEO metadata to that site.
