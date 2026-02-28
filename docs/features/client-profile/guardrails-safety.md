# Guardrails & Safety

**Tier:** Pro | **Type:** Automation / Background

!!! tip "Key Insight"
    Automation without guardrails becomes a liability. These controls are the “seatbelts” that let AlmaSEO run unattended across many sites without turning mistakes into public publishing incidents.

## Overview

Includes:
- Daily cap enforcement
- Duplicate detection via similarity threshold
- Idempotency keys to prevent duplicate jobs/posts on retries
- Race-safe job claiming to support horizontal scaling
- Retry policy with exponential backoff (up to 3 attempts)
- Circuit breaker: pauses a site after repeated failures within a 24h window
- Dead letter queue for jobs requiring manual review

## Why It Matters

Makes it practical to trust automation in production by preventing the most common failure modes: duplicates, bursts, and repeated failing runs.

