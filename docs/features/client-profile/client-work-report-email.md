# Client Work Report Email

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    The preview/send split is a great architecture choice: previews are fast and provider-agnostic, while SendGrid is only required at the final delivery step. Logging the sent report back into the activity stream closes the loop and creates an auditable proof-of-work trail.

## Overview

Inside the Client Profile → Activity & Logs tab, users can select reportable timeline entries using quick-select buttons (**Last 7 Days**, **Last 30 Days**, or **This Billing Period** when retainer tracking is configured), compose a branded email with grouped work items and an optional personal note, preview it (server-rendered HTML via Jinja2), and send it to the client via SendGrid. Each sent report is saved to a work_reports table and logged back into the activity log.

When [Retainer Tracking](retainer-tracking.md) is configured for a site, the report header date range automatically uses the billing period dates (e.g., "Apr 25 - May 24, 2026") instead of the entry date range, so clients see consistent period-based reporting.

## Why It Matters

Makes value visible to clients with a clean “here’s what I did” report, reducing churn risk and saving time writing manual updates.

## Requirements

- **Integrations:** Sendgrid

## Access Control

**Permission Mode:** Configurable per user

