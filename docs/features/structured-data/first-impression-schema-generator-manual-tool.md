# First Impression — Schema Generator (Manual Tool)

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is a low-friction “get schema live today” tool. It pairs naturally with Schema Detection & Scoring: users see what’s missing, then generate the right blocks immediately.

## Overview

Manual, copy/paste Schema Generator embedded inside the First Impression tab (GEO/AI mode). Users open a schema modal to generate schema on demand and copy JSON-LD blocks.

User surface:
- Embedded in First Impression; modal (#schemaGeneratorModal) opens when a schema type is clicked.
- Shows pre-populated schema blocks with Copy buttons.
- Displays Schema Score (0–100) from site scan.

Generation & delivery:
- On-demand via AJAX calls to /api/sites/<site_id>/schema/generate and /api/sites/<site_id>/schema/generate-local-business.
- Output displayed in a <pre> code block with Copy button.
- Not stored in DB and not injected automatically (user copy/pastes into the site).

Schema types:
- LocalBusiness (industry subtype mapping + aggregateRating when available)
- FAQPage
- Service
- BreadcrumbList
- HowTo
- Organization

Primary inputs:
- Client Profile NAP
- Industry field (@type mapping)
- Site URL, email, social links
- User-entered modal fields (hours, services, FAQ pairs)
- GBP rating/review count (from cache) for aggregateRating

## Why It Matters

Lets users quickly generate and copy valid schema markup to improve rich result eligibility without needing a developer.

## Target Audience

Agencies, DIY Business Owners, Freelancers

