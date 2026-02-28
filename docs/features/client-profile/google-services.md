# Google Services

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Google Services is a real parent dropdown in the Client Profile UI. It works as the “Google control center”: one shared connection pattern across multiple Google products, while each child tab delivers a distinct outcome (SEO backbone via Search Console, visibility via Analytics, local presence via Business Profile, paid growth levers via Ads, and content QA via NLP-powered scoring). Keeping this as a parent feature prevents setup duplication and makes Google the clearest integration story in AlmaSEO.

## Overview

Child tabs included:
- Search Console: full GSC performance + indexing/technical health dashboard, and the core data backbone for AlmaSEO’s content strategy and recovery workflows.
- Analytics: GA4 reporting dashboard for traffic and engagement visibility (read-only, standalone; not used as an input to the SEO engine).
- Business Profile: connect and manage Google Business Profile (GBP) to support local SEO workflows and location-aware optimization.
- Google Ads: connect and manage Google Ads with lightweight campaign/keyword/ad creation plus reporting, keyword planner, and SerpAPI fallback only when Ads is not connected.
- Content AI: connect Google Natural Language API (NLP) via OAuth for credential management; enables an inline content quality score across content elsewhere in the platform (quota is tied to the cloud project, not the connecting user).

## Why It Matters

Gives users one consistent place to connect, troubleshoot, and use the client’s Google stack, so AlmaSEO can turn Google data into actionable SEO work without constant tool switching.

## Requirements

- **Integrations:** Google API

## Target Audience

Agencies, DIY Business Owners, Freelancers

## Sub-features

- **[Search Console](search-console.md)** *(Pro)* — Full Google Search Console (GSC) dashboard and data backbone for AlmaSEO’s content strategy.

What it shows:
1) Connection Status: connected proper...
- **[Analytics](analytics.md)** *(Pro)* — Full GA4 reporting dashboard (google_analytics.html, ~1,650 lines) with 5 sub-tabs plus compare mode.

What it shows:
- Overview (default): last-30...
- **[Google Ads](google-ads.md)** *(Agency)* — Google Services child tab for connecting and managing Google Ads for a client profile. Requires OAuth connection (adwords scope) plus a Google Ads ...
- **[Content AI](content-ai.md)** *(Pro)* — Google Services child tab that only handles connecting (and disconnecting) the Google Natural Language API (NLP) for the client via OAuth (same cre...
- **[Business Profile](business-profile.md)** *(Pro)* — Google Services child tab for connecting and managing Google Business Profile (GBP) for the client’s locations.

