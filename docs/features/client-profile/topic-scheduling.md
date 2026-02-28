# Topic Scheduling

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This is a planning UI, not a “job queue.” Saving stores topics, and the scheduler is the bridge between planning and execution. That separation makes the system safer and more predictable.

## Overview

On Save, topics are scored for similarity against existing content. High-similarity topics can be blocked or saved with an explicit override confirmation. Accepted topics are stored as planned topics. When a planned topic’s scheduled date arrives, the scheduler bridge converts it into an automation_jobs entry so it can be executed and tracked in Monitoring.

## Why It Matters

Turns “what should we publish next?” into a simple calendar/queue, so automated publishing stays intentional rather than random.

## Requirements

- **Integrations:** OpenAI API, Wordpress API
- **Compatibility:** Wordpress

