# Content AI

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    The tab itself is intentionally minimal: the product value is the NLP-powered quality score embedded directly into day-to-day content workflows, not another dashboard. Keeping this as a connection toggle prevents duplicated UX, while still letting users clearly see whether Google NLP scoring is enabled.

## Overview

How OAuth is used here (important nuance):
- Unlike GSC / GA / Ads, OAuth is not primarily granting access to the user’s own data.
- It is used for credential management so the app can authenticate against Google Cloud’s Natural Language API.
- NLP analysis consumes the connected cloud project’s quota regardless of which user performed the connection.

What this tab does:
- Connection toggle for Google NLP.
- Stores the connection state used by the rest of AlmaSEO’s content system.

Where the value shows up (not in this tab):
- The actual NLP-driven functionality is surfaced elsewhere in the product (for example, on the post/content details experience), as an inline content quality score shown across content throughout the platform.

Notes / constraints:
- This is not a content generation UI. It is a connection/settings surface that enables NLP scoring features elsewhere.

## Why It Matters

Provides a simple “on/off” connection for Google NLP so AlmaSEO can show an inline quality score on content across the platform.

## Requirements

- **Integrations:** Google API

## Target Audience

Agencies, Freelancers

