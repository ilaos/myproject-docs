# First Impression Tool

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This feature blends automated capture, AI scoring, and verification into a tight improvement loop: run a report, execute action items, re-run to prove what changed, and watch the projected score climb. The GEO mode also creates a bridge from traditional UX into structured-data and entity clarity improvements that support AI-driven discovery.

## Overview

### Analysis Modes

- **UX Analysis** (`ux_only`): Visual homepage audit — eye journey, layout clutter, color harmony, CTA clarity, trust signals, mobile readiness, Core Web Vitals performance.
- **GEO/AI Search Optimizer** (`llm_visibility`): Evaluates readiness for AI-driven search engines (ChatGPT, Perplexity, Google AI Overviews) — entity clarity, structured data, citation-worthiness, AI crawler access, llms.txt protocol. See dedicated docs: [GEO/AI Search Optimizer](geo-ai-search-optimizer.md).

### Pipeline (9 phases)

1. **Init:** Validate URL, load site config, determine fetch mode (AUTO/HTTP/BROWSER).
2. **Screenshot capture:** Playwright headless browser or HTTP fallback. Generates desktop (1920x1080) and mobile (375x812) screenshots. Captures raw HTML and basic speed metrics (TTFB, page size).
3. **PageSpeed audit:** Runs Google PageSpeed Insights v5 against the URL. Captures Lighthouse performance + SEO scores (0-100), Core Web Vitals (LCP, CLS, TBT, FCP) with both lab and real-user CrUX field data, LCP-specific fix opportunities ranked by estimated savings, and Lighthouse SEO pass/fail checks. Performance data is injected into the AI prompt as ground truth so GPT-4o can reference specific CWV numbers in its UX recommendations.
4. **GEO analysis:** Schema extraction, content structure scoring, E-E-A-T signals, AI crawler robots.txt audit (14 bots), llms.txt protocol check. Results cached 24 hours by content hash.
5. **PAA extraction (GEO mode only):** Fetches real People Also Ask questions from Google via DataForSEO to ground FAQ suggestions in actual search data.
6. **Verification:** On re-runs, compares old vs new screenshots via GPT-4o to verify whether prior action items were implemented (FIXED / PARTIALLY_FIXED / NOT_FIXED).
7. **AI analysis:** GPT-4o Vision receives screenshot + ground-truth data (head metadata, PageSpeed/CWV metrics, GEO analysis when applicable) and scores 7-9 categories. 60s timeout; up to 3 retries (2 with image, 1 text-only fallback on moderation).
8. **Action items:** Prioritized checklist (high/medium/low) with preserved completion state across reports.
9. **Storage & error handling:** Saves reports + action items to two tables; graceful fallbacks with user-friendly messages and structured error metadata.

### UX Mode Scoring Categories

7 categories scored 0-100 by GPT-4o:

1. **Above the Fold** — viewport usage, value proposition visibility, key missing elements
2. **Hero Section** — headline quality, value proposition, CTA presence and text
3. **Visual Design** — color scheme, typography, whitespace, brand consistency
4. **Navigation** — menu clarity, accessibility, structure
5. **Trust Signals** — testimonials, certifications, contact info, social proof
6. **Mobile Readiness** — anticipated mobile issues from desktop view
7. **Conversion Potential** — CTA effectiveness, friction points, suggested CTA text

Overall score is GPT-4o's composite assessment (0-100).

### PageSpeed & Core Web Vitals (new)

Added to every analysis (UX and GEO modes):

- **Performance score** (0-100) from Lighthouse
- **Core Web Vitals:** LCP, CLS, TBT, FCP with pass/fail status badges
- **Real-user CrUX data** when available (URL-level or origin-level, embedded in PSI response for free)
- **LCP fix opportunities** ranked by estimated ms savings
- **Lighthouse SEO checks** that are failing (tap targets, font sizes, viewport, etc.)
- Performance data injected into GPT-4o prompt — AI can now say "LCP is 3.2s, optimize the hero image (save ~1.2s)" instead of generic speed advice
- Displayed in dedicated "Page Speed & Core Web Vitals" card in results

### Action Items Checklist

- Grouped by category (Top Priority, Hero Section, Visual Design, Navigation, Trust Signals, Mobile, Conversion).
- Badges: Impact, Effort, Score impact (+5/+3/+1), and Verification status on reruns.
- Instant-save checkbox with toast feedback; failed saves revert automatically.
- Export as CSV and completion progress; projected score updates in real time.

### Progress & Rate Limits

- Frontend polls with exponential backoff (2s → 10s max) and stops after ~5 minutes with retry option.
- Rate limiting: max 3 concurrent reports per site (MAX_CONCURRENT_FI_REPORTS) with queue messaging.

## Why It Matters

Provides a fast, repeatable homepage audit that turns "first impression" UX and AI-search readiness into a prioritized, trackable checklist, so teams can improve clarity, trust, and conversion without guessing. The PageSpeed integration ensures performance recommendations are grounded in real Lighthouse data rather than AI speculation.

## Requirements

- **Required:** OpenAI API (GPT-4o Vision)
- **Optional:** DataForSEO (PAA extraction for GEO mode, ~$0.003/analysis)
- **Depends On:** Site Profile (URL), Playwright or HTTP for page capture

## Cost Per Analysis

| Component | Cost |
|-----------|------|
| GPT-4o Vision analysis | ~$0.03-0.08 |
| PageSpeed Insights | Free |
| Page capture (Playwright/HTTP) | Free |
| PAA extraction (GEO mode, DataForSEO) | ~$0.003 (optional) |

## Backend Modules

| Module | Purpose |
|--------|---------|
| `jobs/first_impression_processor.py` | Main processing pipeline (9 phases) |
| `jobs/visual_capture.py` | Page capture (Playwright + HTTP fallback) |
| `analysis/ai_visual_analysis.py` | AI prompt construction + GPT-4o call |
| `analysis/first_impression.py` | Heuristic fallback analyzer |
| `analysis/schema_parser.py` | JSON-LD / microdata extraction |
| `analysis/content_structure.py` | Content structure + authority analysis |
| `utils/seo_technical.py` | PageSpeed audit, AI bots audit, llms.txt check |
| `utils/seo_serp_intel.py` | PAA extraction (GEO mode) |

## Database Tables

| Table | Purpose |
|-------|---------|
| `first_impression_reports` | Report records with status, scores, screenshots, raw metrics |
| `first_impression_action_items` | Checkable recommendations with verification tracking |
