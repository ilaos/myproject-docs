# GEO/AI Search Optimizer

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tool is “AI discovery readiness” packaged as execution: it grounds the model in real HTML facts, then outputs changes users can implement immediately (rewrites + JSON‑LD). The ground-truth layer keeps recommendations specific and reduces generic AI advice, while the scoring makes progress measurable across schema, structure, and authority.

## Overview

Comprehensive analysis tool that evaluates how visible and extractable a website is to AI-powered search engines (ChatGPT, Claude, Perplexity, Google AI Overviews). Combines automated HTML parsing (“ground truth”) with GPT‑4o Vision analysis to produce prioritized, copy‑paste‑ready improvements, including rewrites and ready-to-use schema markup.

3-layer pipeline:
1) Automated HTML parsing (ground truth):
- Schema markup: detects 10 schema types (FAQPage, LocalBusiness, Organization, HowTo, Article, Service, Review, Breadcrumb, Product, Person). Extracts actual FAQ questions, NAP data, and ratings.
- Content structure: heading hierarchy validity, paragraph quality (optimal/too long/too short), formatting elements (lists, tables, blockquotes), TL;DR presence, FAQ section detection.
- Answer positioning: checks whether first 100 words contain a direct answer vs fluff; detects 18 filler patterns.
- Authority (E‑E‑A‑T): external links (counts .gov/.edu separately), citations, statistics/data points, expert credentials, source attributions.
2) GPT‑4o Vision analysis: receives screenshot + ground-truth data + business context (name, services, location from site profile). Prompt requires using actual page content and business context (no placeholders).
3) Scoring & recommendations: combines parsed facts and AI output into scores, priorities, and ready-to-use content.

GEO scoring (0–100): GEO = (Schema × 35%) + (Content Structure × 50%) + (Authority × 15%). Grade: A (80+), B (65–79), C (50–64), D (35–49), F (<35). Includes detailed sub-scores for Schema, Content Structure, and Authority.

AI category scores (0–100 each): Structured Data & Schema, Content Hierarchy, FAQ Structure, Extractable Content, Entity Clarity, E‑E‑A‑T Signals, Conversational Readiness.

User-facing UI sections:
- Header: GEO, Schema, and Content Structure score circles; readiness badge; executive summary.
- Quick Wins: current vs suggested text with one-click copy, section badges, time estimates, impact statements, and completion checkboxes.
- Specific rewrites (copy/paste): H1, opening paragraph, meta description (~155 chars), heading rewrites, TL;DR suggestion.
- Generated schema markup: ready-to-use JSON‑LD blocks for LocalBusiness, FAQPage, and Service (per main service), with copy buttons.
- Top Priorities: ranked strategic issues with “why it matters,” impact, section, and time estimate.
- Suggested FAQs: Q + A + why it helps, with copy buttons.
- GEO Technical Analysis: schema detection (found vs missing + generate buttons), content structure breakdown, authority signals, and prioritized recommendations.
- Export: copy GEO summary + print report.

Smart prompt engineering: conditional instructions based on parsing results (vague headings, fluff openings, missing schemas, FAQ without FAQPage schema) and requires real business data from the site profile.

Caching: HTML parsing results cached 24 hours by content hash; skips re-parsing if the page has not changed.

## Why It Matters

Turns AI-search visibility into a practical checklist of fixes, with copy-paste rewrites and schema blocks that help a page become easier for AI systems to understand, cite, and answer from.

## Requirements

- **Integrations:** OpenAI API
- **Depends On:** First Impression — Schema Generator, Structured Data

