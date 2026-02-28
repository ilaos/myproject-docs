# Domain & DNS

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tab turns “tribal knowledge” (who owns the domain, where DNS lives, what records exist) into durable, auditable data. The scan-fed detection reduces manual drift and helps agencies catch misconfigurations before they break email, SSL, or site uptime.

## Overview

Tracks / fields:
- Domain: domain name, registrar, registration date, renewal date, auto-renew status, registrar account URL, notes.
- DNS: DNS provider, nameservers, DNS records.

Actions:
- Add / edit / delete domain entries and DNS entries (form-based CRUD).
- Auto-populates detected nameservers and DNS records (A, CNAME, MX, NS) from infrastructure scans into the relevant infrastructure tables.

## Why It Matters

Keeps domain and DNS ownership details in one place and continuously validates them against real scan data, making renewals and DNS troubleshooting faster and less error-prone.

