# Schema Detection & Scoring (Background Analysis)

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    This is the diagnostic side of schema: it turns an invisible technical topic into a measurable score and concrete next steps, which then funnels into the manual generator for quick wins.

## Overview

Background analysis that detects existing structured data on a site and produces a Schema Score plus recommendations used by First Impression.

User surface:
- Not directly visible as a standalone screen.
- Feeds First Impression’s Schema Score (0–100) and pre-populated schema recommendations/needed flags.

Detection & delivery:
- Runs automatically during First Impression processing.
- schema_http://parser.py scans raw HTML and extracts schema markup from JSON-LD <script> tags and microdata.
- Results stored in First Impression analysis output (not separate schema tables).

Schema types detected:
- FAQPage, LocalBusiness, HowTo, Organization, Breadcrumb, Article, Service, Review, Product, Person.

Primary inputs:
- Raw HTML of analyzed pages
- Existing JSON-LD and microdata markup

## Why It Matters

Shows users what schema they already have, what they’re missing, and how strong their structured data footprint is—without manual inspection.

## Target Audience

Agencies, DIY Business Owners, Freelancers

