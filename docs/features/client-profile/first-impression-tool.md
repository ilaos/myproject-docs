# First Impression Tool

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This feature blends automated capture, AI scoring, and verification into a tight improvement loop: run a report, execute action items, re-run to prove what changed, and watch the projected score climb. The GEO mode also creates a bridge from traditional UX into structured-data and entity clarity improvements that support AI-driven discovery.

## Overview

Analysis modes:
- UX Analysis: visual homepage audit (eye journey, layout clutter, color harmony, CTA clarity, trust signals, mobile readiness).
- GEO/AI Search Optimizer: evaluates readiness for AI-driven search engines (ChatGPT, Perplexity, Google SGE) focusing on entity clarity, structured data, and citation-worthiness.

Pipeline (8 phases):
1) Init: validate URL, load site config.
2) Screenshot capture: Playwright headless browser or HTTP fallback with fetch modes AUTO / HTTP_ONLY / BROWSER_ONLY. Generates placeholder images if capture fails.
3) GEO analysis: schema extraction, content structure scoring, E‑E‑A‑T signals. Cached 24 hours by content hash.
4) Verification: on re-runs, compares old vs new screenshots via GPT‑4o to verify whether prior action items were implemented (FIXED / PARTIALLY_FIXED / NOT_FIXED).
5) AI analysis: GPT‑4o Vision scores 6 UX categories (1–10). 60s timeout; up to 3 retries on moderation refusals.
6) Action items: prioritized checklist (high/medium/low) with preserved completion state across reports.
7) Storage: saves reports + action items to two tables; DB connections use try/finally safeguards.
8) Error handling: graceful fallbacks with user-friendly messages and structured error metadata.

Action items checklist UI:
- Grouped by category (Top Priority, Hero Section, Visual Design, Navigation, Trust Signals, Mobile, Conversion).
- Badges: Impact, Effort, Score impact (+5/+3/+1), and Verification status on reruns.
- Instant-save checkbox with toast feedback; failed saves revert automatically.
- Export as CSV and completion progress; projected score updates in real time.

Scoring:
- 6 categories: Visual Hierarchy & Eye Flow, Content Clarity & Messaging, Trust Signals & Social Proof, CTA Effectiveness, Mobile Responsiveness Indicators, Brand Consistency & Professionalism.
- Overall score is a weighted average displayed as letter grade (A–F).

Progress + limits:
- Frontend polls with exponential backoff (2s → 10s max) and stops after ~5 minutes with retry option.
- Rate limiting: max 3 concurrent reports per site (MAX_CONCURRENT_FI_REPORTS) with queue messaging.

## Why It Matters

Provides a fast, repeatable homepage audit that turns “first impression” UX and AI-search readiness into a prioritized, trackable checklist, so teams can improve clarity, trust, and conversion without guessing.

## Requirements

- **Integrations:** OpenAI API
- **Depends On:** SEO Recovery 911, First Impression — Schema Generator

