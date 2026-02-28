# Opportunities

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tab is the handoff point from verification to growth. Auto-generating high-fit opportunities from lost links is a strong lever because it focuses effort on warm targets (they linked once already), and it keeps the outreach pipeline continuously replenished as the backlink set changes.

## Overview

How opportunities are created:
- Auto from lost backlinks: when verification marks a backlink as lost, an opportunity is auto-created with fit_score=70 and status=new (high priority because the site has linked before).
- Manual: Add Opportunity lets users enter a source URL and optional details; status=new; fit score not set by default.
- CSV import: imported backlinks become verification targets; lost ones generate opportunities via the auto rule above.

Opportunity pipeline stages (shared with Outreach kanban): New → Queued → Reached → Won, with Lost as an alternate terminal state. “Reached” is set automatically when an email is sent.

Opportunities tab UI:
- Dashboard cards: Unique Domains, Total Backlinks, Live Links, Lost Links, Pending Verification.
- Imported backlinks table: Status, Domain, Source URL, Anchor Text, Target URL, Imported On, with color-coded badges (live/lost/pending).
- Bulk action: Verify Links Now (checks up to 10 at a time).
- Onboarding callout: emphasizes that sites that already linked are the easiest outreach targets; references a future Prospects feature for non-linking sites.

## Why It Matters

Creates a clear, prioritized list of link opportunities (especially lost links) so teams can move from backlink monitoring into targeted outreach without manual triage.

## Requirements

- **Integrations:** Sendgrid

