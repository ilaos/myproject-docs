# Client Work Report Email

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    The preview/send split is a great architecture choice: previews are fast and provider-agnostic, while SendGrid is only required at the final delivery step. Logging the sent report back into the activity stream closes the loop and creates an auditable proof-of-work trail.

## Overview

Inside the Client Profile → Activity & Logs tab, users can select reportable timeline entries (or auto-select the last 7 days), compose a branded email with grouped work items and an optional personal note, preview it (server-rendered HTML via Jinja2), and send it to the client via SendGrid. Each sent report is saved to a work_reports table and logged back into the activity log.

## Why It Matters

Makes value visible to clients with a clean “here’s what I did” report, reducing churn risk and saving time writing manual updates.

## Requirements

- **Integrations:** Sendgrid

## Access Control

**Permission Mode:** Configurable per user

