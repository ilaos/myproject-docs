# Email Providers

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Email breakage is one of the fastest ways to erode client trust. By surfacing scan-validated SPF/DKIM/DMARC status next to provider/renewal details, this tab supports both proactive security and practical operations.

## Overview

Tracks / fields:
- Email provider, plan, admin console URL
- Mailbox count, monthly cost, renewal date, notes
- MX records, SPF record
- DKIM configured (boolean), DMARC configured (boolean)

Actions:
- Add / edit / delete email entries (form-based CRUD).
- Auto-detects MX records and validates SPF/DKIM/DMARC status from infrastructure scans.

## Why It Matters

Makes email infrastructure explicit and verifiable, reducing deliverability issues and preventing forgotten renewals or misconfigurations during DNS changes.

