# SSL & Security

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Separating “certificate management” (this tab) from “security posture” (headers in Scan Overview) keeps the UX clean: this is the place to own expiry and issuer details, while the dashboard tells you what to fix first.

## Overview

Tracks / fields:
- Certificate issuer, certificate type
- Domains covered, SAN domains
- Valid from/to dates, auto-renew status
- Managed by, last checked date
- Validity status, check errors, notes

Actions:
- Add / edit / delete SSL entries (form-based CRUD).
- Auto-populates issuer, expiry, and validity signals from infrastructure scan SSL/TLS checks.

## Why It Matters

Keeps SSL certificate ownership and renewal details organized, and uses scan data to catch invalid or expiring certificates early.

