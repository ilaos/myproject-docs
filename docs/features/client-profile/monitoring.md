# Monitoring

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Monitoring is where trust is earned. The ability to review failures and retry/remove them per job is what makes scheduled publishing feel manageable rather than opaque.

## Overview

Job traceability:
- Jobs created from Content Planning show a “Planned” badge.
- Job detail includes the source and original topic text.

Quality visibility:
- Quality scores are shown as color-coded badges in the Monitoring UI.

Access control (admin-only):
- DLQ bulk actions, queue management controls, and runtime flags are restricted to admins.
- Per-job recovery actions like Retry/Remove should be treated as admin actions when admin gating is enabled.

## Why It Matters

Gives users clear visibility into what ran, what is running, and what failed, with straightforward recovery actions and a fast path to finish posts with a featured image.

## Requirements

- **Integrations:** OpenAI API, Wordpress API
- **Compatibility:** Wordpress

