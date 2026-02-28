# Hosting

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Hosting is often the root cause of performance and reliability problems. By pairing “what we think the hosting is” (manual records) with “what the internet sees” (scan detection), this tab reduces surprises during incident response and migrations.

## Overview

Tracks / fields:
- Hosting provider, plan name, plan type
- IP address, server location
- Monthly cost, renewal date, contract end date
- cPanel URL, SSH/SFTP access
- PHP version, MySQL version, WordPress version
- Notes

Actions:
- Add / edit / delete hosting entries (form-based CRUD).
- Auto-detects hosting provider and IP address from infrastructure scans and surfaces those values alongside the stored records.

## Why It Matters

Provides a single place to document hosting access and lifecycle details (costs, renewals, contracts) while using scans to confirm the real hosting/IP footprint of the site.

