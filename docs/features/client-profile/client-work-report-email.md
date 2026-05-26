# Client Work Report Email

**Tier:** Pro/Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    The preview/send split is a great architecture choice: previews are fast and provider-agnostic, while SendGrid is only required at the final delivery step. Logging the sent report back into the activity stream closes the loop and creates an auditable proof-of-work trail.

## Overview

Inside the Client Profile → Activity & Logs tab, users can select reportable timeline entries using quick-select buttons (**Last 7 Days**, **Last 30 Days**, **This Billing Period**, or **Last Billing Period** when retainer tracking is configured), compose a branded email with grouped work items and an optional personal note, preview it (server-rendered HTML via Jinja2), and send it to the client via SendGrid. Each sent report is saved to a work_reports table and logged back into the activity log.

When [Retainer Tracking](retainer-tracking.md) is configured for a site, the report header date range automatically uses the billing period dates (e.g., “Apr 25 - May 24, 2026”) instead of the entry date range, so clients see consistent period-based reporting.

## Why It Matters

Makes value visible to clients with a clean “here’s what I did” report, reducing churn risk and saving time writing manual updates.

## Compose Modal Options

The compose modal provides the following fields and options:

### Recipient & Sender

| Field | Description |
|-------|-------------|
| **Recipient Email** | The client’s email address. Pre-filled from site business info if available. |
| **Sender Name** | Display name shown in the client’s inbox (e.g., “John Smith”). Remembered across sessions. |
| **Reply-To** | Where client replies go instead of support@almaseo.com. Remembered across sessions. |
| **CC** | Comma-separated email addresses to copy on the report. Visible to all recipients. |
| **BCC** | Comma-separated email addresses to blind copy. Hidden from other recipients. |
| **Subject** | Auto-generated from site name and month, or customizable. |
| **Personal Note** | Optional message displayed at the top of the email. |

### Report Options

| Option | Description |
|--------|-------------|
| **Plain email style** | Renders a simple email that reads like a personal message instead of the branded template. |
| **Hide dates** | Removes date labels from individual entries and the header date range. |
| **Hide hours** | Removes duration badges from entries and the total time from the summary bar. |
| **Include retainer usage** | Shows retainer budget status in the summary bar. Only visible when [Retainer Tracking](retainer-tracking.md) is configured. |

### Retainer Budget in Reports

When “Include retainer usage” is enabled, the summary bar at the top of the email shows hours logged vs. the retainer budget:

- **Under budget:** `15h 15m logged (4h 45m of 20h budget remaining)` (green)
- **Over budget:** `15h 15m logged (+10h 15m over 5h budget)` (red, bold)

The hours are calculated from the actual entries included in the report, so it works correctly for both current and past billing periods.

### Selection Summary Tray

When entries are selected for a report, a summary tray appears above the timeline showing every selected entry grouped by category. Each entry has a remove button, allowing you to deselect individual items without scrolling through the timeline to find them.

### Included Items List

The compose modal displays all selected items grouped by category with individual remove buttons, so you can fine-tune the report contents before sending.

## Draft Autosave

All compose modal fields (recipient, sender name, reply-to, CC, BCC, subject, personal note, and all toggle options) are automatically saved to browser local storage per site. Drafts are restored when reopening the compose modal and cleared after a successful send.

## Requirements

- **Integrations:** SendGrid

## Access Control

**Permission Mode:** Configurable per user

