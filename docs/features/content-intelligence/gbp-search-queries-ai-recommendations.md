# GBP Search Queries → AI Recommendations

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    High-leverage signal: GBP search queries are bottom-of-funnel intent from real customers. When combined with GSC momentum and other market context, AlmaSEO can recommend topics that match proven demand instead of guessing. Cache-first design minimizes added latency and degrades gracefully when GBP data is unavailable.

## Overview

What it does:
- When users request blog topic suggestions, the prompt context now includes top GBP search queries (keywords) with impression counts, representing how real customers find the business on Google Maps/Search.
- The model is instructed to prioritize topics that match these GBP search terms.

Data flow / implementation:
- build_live_market_context() now includes GBP search queries (top ~7 keywords with impressions) alongside existing signals (e.g., GSC momentum keywords, industry news, seasonal context).
- Helper: fetch_gbp_search_queries_for_ai(site_id)
	- Uses GBP cache first (5-minute TTL).
	- If not cached, fetches via GBP Performance API using stored location info/credentials.
	- Tries the last 3 months (to account for reporting delays).
	- Returns up to 10 keywords sorted by impressions.
	- Populates the cache on fresh fetch.
- Wrapped in try/except so recommendations still work if GBP fails.

Prompt additions:
- Instruction: if GBP trends are present, prioritize them as real demand signals.
- Topic mix category: “Topics matching GBP customer search terms (proven demand) [EVERGREEN]”.

## Why It Matters

Produces blog topic recommendations that align with what customers are already searching for on Google, increasing relevance and likelihood of driving demand.

## Requirements

- **Integrations:** Google API, OpenAI API
- **Depends On:** Business Profile

## Target Audience

Agencies, DIY Business Owners, Freelancers

