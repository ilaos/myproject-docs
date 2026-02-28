# Content Automation

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Content Automation is one purpose, executed reliably. The key product value is the combination of planning + operational safety: planned topics flow into jobs via a scheduler bridge, duplicates are surfaced and can be explicitly overridden, and monitoring makes execution observable. Visible quality badges and “Planned” traceability close the loop from planning to execution. Admin-only queue/DLQ controls prevent accidental system-wide actions.

## Overview

UI structure (sub-tabs):
- Content Planning: generate topic ideas, add custom topics, reorder topics, and select which ones to schedule. On save, topics are scored for similarity, duplicates can be blocked or overridden by confirmation, and accepted topics are stored as the plan.
- Settings: start date, schedule duration (weeks), draft vs auto-publish, preferred publish time, and post-ready email notifications. Posting frequency and daily caps are user-configurable here.
- Monitoring: recent jobs, job detail, queue health, and failed job review (DLQ). Jobs created from Content Planning are traceable and show a “Planned” badge plus the original topic/source in job details. Completed jobs with a WordPress post show a “Generate” action to open the featured image generator modal and upload an image directly to the post.

Execution pipeline (when a topic runs): plan is saved → scheduler bridge converts due planned topics into automation_jobs → guardrail checks → AI article generation (can include GBP review testimonials if available) → quality scoring (visible as color-coded badges) → WordPress publish (draft or live) → optional IndexNow submission → optional email notification → activity/log updates.

Access control note: DLQ, queue controls, and runtime flags are admin-only.

## Why It Matters

Lets users maintain a consistent publishing cadence with minimal manual effort: plan topics once, then have AlmaSEO generate and publish WordPress posts on schedule, with strong duplicate prevention, clear monitoring, and a built-in featured image workflow for completed posts.

## Requirements

- **Integrations:** OpenAI API, Wordpress API

## Sub-features

- **[Topic Scheduling](topic-scheduling.md)** *(Pro)* — Content Planning sub-tab surface for building a per-site publishing plan. Users can generate topic ideas via AI (magic wand), add custom topics man...
- **[Automation Settings](automation-settings.md)** *(Pro)* — Settings sub-tab surface for per-site automation configuration. Users toggle content automation on/off for a specific site and control how schedule...
- **[Monitoring](monitoring.md)** *(Pro)* — Monitoring sub-tab surface for observing automation activity for a single site. Shows recent jobs, job details, queue status, and failed job review...
- **[Content Pipeline](content-pipeline.md)** *(Pro)* — End-to-end automation workflow that generates and publishes content for a site.

Pipeline steps:
1) Guardrail checks (daily cap, duplicates, circui...
- **[Guardrails & Safety](guardrails-safety.md)** *(Pro)* — Reliability and safety mechanisms that prevent over-publishing, duplicates, and runaway failure loops in automated publishing.

Includes:
- Daily c...
- **[Monitoring & Logs](monitoring-logs.md)** *(Pro)* — Operational visibility for automation across sites. Provides per-job logs and system health indicators so users and admins can understand what ran,...

