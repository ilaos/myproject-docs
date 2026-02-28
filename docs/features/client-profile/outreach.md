# Outreach

**Tier:** Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is a full outreach engine inside AlmaSEO: it turns backlink gaps into a trackable pipeline with measurable outcomes (deliverability, engagement, wins) and automation (sequences + stop logic). The webhook-driven feedback loop plus safety limits make it viable for agencies to run campaigns without external tooling.

## Overview

Kanban pipeline (4 columns):
- New (gray): fresh opportunities, not yet contacted.
- Queued (yellow): scheduled for outreach; email not yet sent.
- Reached (blue): email sent; waiting for response (opportunity auto-moves here on send).
- Won (green): link earned/confirmed.

Opportunity card shows:
- Domain (clickable), anchor text (if available), “Lost Link” badge (if auto-created from verification), notes indicator.
- Live email status: Sent, Delivered, Opened (green), Clicked (blue), Bounced (red).
- Actions: Send Email, Start Sequence, Move Status, View History, Delete.

Outreach metrics dashboard (7 stats): Total Sent, Delivered, Open Rate, Click Rate, Reply Rate, Bounced, Wins (opportunities marked won that had ≥1 email).

Email templates:
- CRUD reusable templates with placeholders url, anchor_text, target_url auto-filled on send.
- Preview before sending; plain text auto-converted to styled HTML.

Email sending + tracking:
- Choose template or write custom, enter recipient email, send via SendGrid (message_id captured).
- POST /sendgrid/webhook receives events and records Delivered/Opened/Clicked/Replied/Bounced with timestamps.
- Email history timeline per opportunity shows send date + all engagement timestamps.

Safety limits:
- 24-hour cooldown per prospect (prevents double-emailing).
- 100 emails/day per site; returns 429 with clear messaging when hit.

Automated sequences (drip campaigns):
- Sequence = named campaign with ordered steps (template, delay; default 72h) and per-step stop conditions.
- Assign sequence to an opportunity + recipient email; step 1 sends immediately; scheduler sends subsequent steps when due.
- Smart stop conditions (default on): stop_on_reply, stop_on_click, stop_on_open; always stop on bounce.

Modals: Add Opportunity, Send Email, Email History, Templates, Sequences, Assign Sequence, Notes (AJAX save).

Search & filter: real-time filtering across source URL, anchor text, and notes; filters visible cards in the kanban view.

## Why It Matters

Lets teams run structured backlink outreach at scale with templates, sequences, and real-time engagement tracking, so link reclamation and link building become repeatable rather than ad hoc.

## Requirements

- **Integrations:** Sendgrid

## Access Control

**Permission Mode:** Configurable per user

