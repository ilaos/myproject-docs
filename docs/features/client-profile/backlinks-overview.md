# Backlinks Overview

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    The verification engine is the backbone: it turns static backlink lists into living, monitored assets. Auto-creating outreach opportunities for lost links converts monitoring into action, making backlinks a repeatable workflow rather than a one-time audit.

## Overview

What the user sees:
- Analytics dashboard cards: Total Backlinks, Unique Referring Domains, Live Links (verified), New This Month.
- CSV import: upload exports from major tools with auto-detection (GSC Links export, Ahrefs, SEMrush, Moz, Majestic, or custom with source_url + target_url). Auto-maps columns, skips duplicates, and reports new/skipped/error counts.
- Bulk verification: Verify All Pending processes up to 10 backlinks per request with a smart priority queue (never-checked first, then live links older than 7 days, then lost links older than 14 days).
- Backlinks table: filter tabs All / Live / Lost / Pending; columns include Status, Source URL, Target URL, Anchor Text, Domain, Last Checked, HTTP status; per-row Verify button.

Verification engine (backlinks_http://verifier.py):
- Fetches source URL (4s timeout, browser UA). If 200, parses HTML (BeautifulSoup) and searches <a> tags for the target URL.
- Matching supports exact URL, domain match, or URL prefix match (handles query string variations).
- If found: status=live and captures anchor text + page title. If not found: status=lost.
- Timeouts/SSL errors are status=error (does not falsely mark as lost).
- Every check is logged in backlink_checks with timestamp, HTTP status, found/not-found, anchor snapshot, and page title.

Auto-outreach trigger:
- When a link is marked lost, automatically creates an outreach opportunity (fit_score=70) because the site has linked before.

## Why It Matters

Gives a single operational dashboard to import backlinks from external sources, keep them verified over time, and quickly identify lost links that should be reclaimed through outreach.

## Requirements

- **Integrations:** Sendgrid

