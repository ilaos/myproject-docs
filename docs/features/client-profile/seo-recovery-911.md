# SEO Recovery 911

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is a “hard conversation” tool: it turns messy performance drops into an explainable audit, a phased plan with budget expectations, and ready-to-send communication templates. The prerequisites (GSC + NAP Shield) ensure the audit is grounded in both search demand/performance and business identity consistency, which are the two fastest levers for local SEO triage.

## Overview

Prerequisites (both required, checked in real time before enabling Run Emergency Audit):
- Google Search Console connected and verified.
- NAP Shield has at least one location scanned.

Audit configuration (modal):
- Primary focus areas (service keywords).
- Geographic focus (cities/counties).
- Exclude terms (competitors, discontinued services).
- Brand search toggle (include/exclude branded queries).

Backend pipeline (90-day GSC window):
1) Fetch raw GSC query data (clicks, impressions, position).
2) Filter by user config (focus/geo/exclusions/brand).
3) Optional: enrich with search volume when Google Ads is connected.
4) Analyze dead-zone keywords, practice area breakdown, and brand vs non-brand split.
5) Optional: pull GBP audit data (category recs, review stats) when GBP is connected.
6) Pull NAP Shield data (health score, conflicts, inconsistencies).
7) Detect issues/opportunities via thresholds (CTR, position, dead-zone count, brand dependency, NAP health, wrong keyword focus).
8) Persist audit results to database.

Issue detection thresholds (examples): CTR <1% warning / <0.5% critical; avg position >20 warning / >50 critical; dead-zone keywords critical when >20 in positions 15–70; brand dependency warning when >80% clicks from brand; NAP health <90% warning / <70% critical; wrong keyword focus warning when 5+ top-10 keywords have <50 monthly searches.

6-tab UI:
1) Dashboard: SEO Health Score, Issues, Opportunities + key findings summary.
2) Audit Results: NAP health + conflicts + recommendations; multi-location selector; practice area + brand split; dead-zone keywords (top 50); top-performing keywords.
3) Recovery Plan: plan type selector (Hybrid, SEO Only, Paid Only, Maintenance/Pause) + industry input; GPT-4-turbo 3-phase plan (Months 1–3, 4–6, 7–12) + budget/timeline summary.
4) Audit History: previous audits + compare any two with % deltas.
5) Client Comms: 5 AI email templates with tone selector, editable preview, copy/download/save + comms history table.
6) Reminders: create follow-ups (type/date/note), email notifications + daily digest option, CRUD table (complete/delete/reschedule).

AI generation (GPT-4-turbo): recovery plans + client communications, with template-based fallbacks if AI is unavailable.

Not in scope:
- Page-level content analysis (handled by First Impression).
- Backlink analysis.
- Schema validation (handled by GEO Optimizer).
- WordPress dependency (works with any site that has GSC).

## Why It Matters

Gives agencies a repeatable emergency workflow to diagnose SEO performance issues, generate a credible recovery plan, and communicate clearly with clients using real metrics and structured follow-up.

## Requirements

- **Integrations:** Google API, OpenAI API, Sendgrid
- **Depends On:** Search Console, Business Profile, Google Ads

