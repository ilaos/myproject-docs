# GEO/AI Search Optimizer

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tool is "AI discovery readiness" packaged as execution: it grounds the model in real HTML facts, then outputs changes users can implement immediately (rewrites + JSON-LD). The ground-truth layer keeps recommendations specific and reduces generic AI advice, while the scoring makes progress measurable across schema, structure, and authority.

## Overview

Comprehensive analysis tool that evaluates how visible and extractable a website is to AI-powered search engines (ChatGPT, Claude, Perplexity, Google AI Overviews). Combines automated HTML parsing ("ground truth") with GPT-4o Vision analysis to produce prioritized, copy-paste-ready improvements, including rewrites and ready-to-use schema markup.

### 4-Layer Pipeline

**Layer 1: Automated HTML Parsing (ground truth)**

- Schema markup: detects 10 schema types (FAQPage, LocalBusiness, Organization, HowTo, Article, Service, Review, Breadcrumb, Product, Person). Extracts actual FAQ questions, NAP data, and ratings.
- Content structure: heading hierarchy validity, paragraph quality (optimal/too long/too short), formatting elements (lists, tables, blockquotes), TL;DR presence, FAQ section detection.
- Answer positioning: checks whether first 100 words contain a direct answer vs fluff; detects 18 filler patterns.
- Authority (E-E-A-T): external links (counts .gov/.edu separately), citations, statistics/data points, expert credentials, source attributions.

**Layer 2: AI Crawler & Protocol Checks**

- **robots.txt audit (14 AI crawlers):** Checks access policy for GPTBot, ChatGPT-User, OAI-SearchBot, ClaudeBot, Claude-Web, PerplexityBot, Perplexity-User, Google-Extended, Applebot-Extended, Bytespider, CCBot, FacebookBot, Meta-ExternalAgent, Amazonbot, Diffbot. Identifies critical blocked crawlers and heuristic warnings (e.g., blocking named bots but allowing CCBot). Uses `utils/seo_technical.aibots_audit()` (shared with SEO Recovery 911).
- **llms.txt protocol check:** Verifies presence and structure of `/llms.txt` and `/llms-full.txt` per the [llmstxt.org](https://llmstxt.org) specification. Parses title, summary blockquote, sections, and links. Reports health (green/amber/red) with specific issues (missing title, missing summary, etc.). Sites publishing llms.txt signal AI-readiness to crawlers. Uses `utils/seo_technical.llms_txt_check()`.

**Layer 3: Real SERP Data (optional, DataForSEO)**

- **People Also Ask extraction:** Auto-builds keyword list from site context (business services + location), fetches real PAA questions from Google via DataForSEO advanced SERP endpoint. Injects actual Google questions into the AI prompt so FAQ suggestions are grounded in real search data instead of AI-generated guesses. Cost: ~$0.003/analysis (5 keywords). Gracefully skips if DataForSEO not configured. Uses `utils/seo_serp_intel.extract_paa_questions()`.

**Layer 4: GPT-4o Vision Analysis**

- Receives screenshot + ground-truth data (schema, structure, authority, crawler access, llms.txt status, real PAA questions) + business context (name, services, location from site profile).
- Prompt requires using actual page content and business context (no placeholders).
- Conditional instructions based on parsing results (vague headings, fluff openings, missing schemas, FAQ without FAQPage schema, missing llms.txt).
- When real PAA questions are available, the prompt instructs the model to use them for FAQ suggestions instead of generating generic ones.

### Scoring

**GEO Score (0-100):** Schema (30%) + Content Structure (45%) + Authority (10%) + AI Accessibility (15%).

Grade: A (80+), B (65-79), C (50-64), D (35-49), F (<35).

**AI Category Scores (0-100 each):** Structured Data & Schema, Content Hierarchy, FAQ Structure, Extractable Content, Entity Clarity, E-E-A-T Signals, Conversational Readiness, Content Layout for AI.

### User-Facing UI Sections

- **Header:** GEO, Schema, and Content Structure score circles; AI Search Readiness badge; AI Crawler Access status (14 bots with allowed/blocked badges); llms.txt protocol status; executive summary.
- **Quick Wins:** current vs suggested text with one-click copy, section badges, time estimates, impact statements, and completion checkboxes.
- **Specific Rewrites (copy/paste):** H1, opening paragraph, meta description (~155 chars), heading rewrites, TL;DR suggestion.
- **Content Layout for AI:** Above-fold audit, buried content detection (tabs/accordions), recommended sections to add (Key Facts Bar, FAQ, Trust Bar, etc.), restructuring recommendations.
- **Generated Schema Markup:** Ready-to-use JSON-LD blocks for LocalBusiness, FAQPage, and Service (per main service), with copy buttons.
- **Top Priorities:** Ranked strategic issues with "why it matters," impact level, section, and time estimate.
- **Suggested FAQs:** Q + A + why it helps, with copy buttons. Grounded in real Google PAA data when DataForSEO is configured.
- **GEO Technical Analysis:** Schema detection (found vs missing + generate buttons), content structure breakdown, authority signals, and prioritized recommendations.
- **Export:** PDF report (via WeasyPrint) + copy GEO summary.
- **Progress Tracking:** Action item checklist with completion status, verification on re-analysis (FIXED / PARTIALLY_FIXED / NOT_FIXED).

### Smart Prompt Engineering

Conditional instructions based on parsing results:

- Vague headings detected → requires specific rewrites
- Fluff opening detected → requires direct-answer opening rewrite
- Missing critical schemas → explains competitive advantage of each
- FAQ in HTML but no FAQPage schema → flags critical miss
- No TL;DR → recommends placement and content
- Real PAA questions available → uses them for FAQ generation
- llms.txt missing → recommends creating it

### Caching

HTML parsing results cached 24 hours by content hash; skips re-parsing if the page has not changed.

## Why It Matters

Turns AI-search visibility into a practical checklist of fixes, with copy-paste rewrites and schema blocks that help a page become easier for AI systems to understand, cite, and answer from. The llms.txt check and real PAA data ground recommendations in what AI crawlers and Google actually do, not just what they theoretically could do.

## Requirements

- **Required:** OpenAI API (GPT-4o Vision)
- **Optional:** DataForSEO (real PAA questions from Google, ~$0.003/analysis)
- **Depends On:** First Impression tool (shared infrastructure), Site Profile (business context)

## Cost Per Analysis

| Component | Cost |
|-----------|------|
| GPT-4o Vision analysis | ~$0.03-0.08 |
| HTML parsing, robots.txt, llms.txt | Free |
| PAA extraction (DataForSEO) | ~$0.003 (optional) |

## Backend Modules

| Module | Purpose |
|--------|---------|
| `jobs/first_impression_processor.py` | Main processing pipeline |
| `analysis/ai_visual_analysis.py` | AI prompt construction + GPT-4o call |
| `analysis/schema_parser.py` | JSON-LD / microdata extraction |
| `analysis/content_structure.py` | Content structure + authority analysis |
| `utils/seo_technical.py` | AI bots audit (14 crawlers) + llms.txt check |
| `utils/seo_serp_intel.py` | PAA question extraction from Google |
