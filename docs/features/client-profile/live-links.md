# Live Links

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tab is the credibility layer for backlink reporting. Because “Live” status is tied to repeatable verification + an audit trail, agencies can confidently show what is truly active today, and any flip to “lost” automatically feeds the outreach system for reclamation.

## Overview

Data model:
- Primary table: backlinks (unique constraint on site_id + source_url + target_url). Key fields: source_url, target_url, anchor_text, status (pending/live/lost), last_checked, http_status, domain.
- Audit trail: backlink_checks logs every verification attempt (checked_at, http_status, found, anchor_snapshot, page_title).

UI layout (backlinks_live.html):
1) Dismissible onboarding tip stored in localStorage.
2) Stats dashboard (4 cards): Live Links, Pending Verification, Lost Links, Unique Domains (from backlinks_stats aggregates).
3) Live backlinks table columns:
- Source URL (clickable; truncated with tooltip)
- Target URL
- Anchor Text (badge, first 50 chars)
- Domain
- Last Verified (date + HTTP status badge; green check for 200)
- Actions: Re-verify
4) Empty state directing users back to Overview tab to import backlinks first.

Verification logic (re-verify):
- Single: POST /site/<site_id>/backlinks/<backlink_id>/verify performs HTTP GET to source_url, parses HTML (BeautifulSoup), searches <a href> tags for target_url, then sets status live/lost, updates backlinks, inserts backlink_checks record, and shows a flash message.
- Bulk: POST /site/<site_id>/backlinks/verify_bulk runs a batch of 10 with priority order: never-checked → stale live (>7 days) → lost (>14 days). Reports batch results (e.g., 8 live, 2 lost).

URL matching (backlinks_http://verifier.py): exact normalized match OR domain match OR prefix match (querystring-safe).

Auto-outreach:
- When a backlink flips to lost, auto-creates an outreach opportunity (source_type='lost_backlink', fit_score=70).

Configuration (current defaults): timeout 4s, UA AlmaSEO Backlink Verifier/1.0, max retries 2, batch size 10, recheck intervals live 7d / lost 14d.

## Why It Matters

Gives a clean, trustworthy view of active backlinks so teams can report confirmed wins, monitor the live portfolio over time, and re-verify links when needed without wading through pending/lost noise.

