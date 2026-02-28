# Content Pipeline

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    This is one purpose, executed reliably. The product differentiator is not breadth of “automation types,” but the completeness of the pipeline: generate, validate, publish, notify, and log—every time.

## Overview

Pipeline steps:
1) Guardrail checks (daily cap, duplicates, circuit breaker state)
2) Generate article via AI (business context + SEO focus; may include GBP review testimonials when available)
3) Optional quality analysis (Google NLP scoring; currently recorded for monitoring)
4) Publish to WordPress (draft or publish mode)
5) Optional IndexNow submission (if enabled)
6) Optional email notification (if enabled)
7) Write run details to logs/activity history

## Why It Matters

Delivers consistent publishing without manual drafting and posting, while keeping clear checkpoints and optional add-ons like indexing and notifications.

## Requirements

- **Integrations:** OpenAI API, Wordpress API
- **Compatibility:** Wordpress

