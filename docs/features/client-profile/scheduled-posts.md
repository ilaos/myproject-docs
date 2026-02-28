# Scheduled Posts

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Scheduling is the bridge between content creation and publishing. The duplicate-risk badge makes it more than a calendar: it introduces portfolio-level quality control (avoiding near-duplicate posts) before content goes live.

## Overview

UI elements:
- Total scheduled count badge
- Schedule Content button
- Timeline view (up to 10 posts) showing:
	- Post title + meta description preview
	- Scheduled date
	- Duplicate Risk badge (from automation_topics table): Low/Medium/High with similarity % and closest-match title, or Not analyzed
	- Keyword badge (if set)
	- Edit and Cancel buttons (currently stubs; not wired to backend)

## Why It Matters

Provides a lightweight editorial calendar view so users can plan upcoming content, spot duplication risk early, and keep scheduled work organized per client.

## Requirements

- **Integrations:** Google API, OpenAI API, Wordpress API

