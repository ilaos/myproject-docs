# Reviews → Content Mining for Blog Topics

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    This is “VOC-driven content strategy” baked into the engine. Reviews contain bottom-of-funnel objections and service expectations; mining them helps AlmaSEO recommend topics that answer what customers actually worry about (and what the business is praised/criticized for). Cache-first + truncation keeps it fast and prompt-friendly.

## Overview

How it works:
- Trigger: user requests AI Recommendations.
- build_live_market_context() calls fetch_gbp_reviews_for_ai(site_id).
- Collects reviews that contain text (filters out star-only ratings).
- Injects up to ~7 review snippets into the GPT-4 prompt (each truncated to ~150 characters) under a “Customer Review Insights” section.
- Model mines patterns across snippets and prioritizes topics that directly address real customer concerns.

Helper function: fetch_gbp_reviews_for_ai(site_id)
- Uses GBP reviews cache first (so there is no extra latency if the GBP tab was viewed recently).
- If not cached, loads location + credentials and fetches via the GBP reviews endpoint (v4), then caches results.
- Returns up to ~15 reviews with text, rating, and author.

Prompt additions:
- Instruction: if review insights are present, mine for recurring themes/pain points/questions for content ideas.
- Topic mix category: “Topics addressing pain points or themes found in customer reviews [EVERGREEN]”.

Design note:
- 150-character snippet truncation preserves token budget while still capturing themes (response time, scheduling friction, mold concerns, professionalism, etc.).

## Why It Matters

Generates blog topics that reflect the real voice of customers, making content more relevant, empathetic, and likely to convert.

## Requirements

- **Integrations:** Google API, OpenAI API
- **Depends On:** Business Profile

## Target Audience

Agencies, DIY Business Owners, Freelancers

