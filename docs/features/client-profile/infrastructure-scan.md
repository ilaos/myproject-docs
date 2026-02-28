# Infrastructure Scan

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Infrastructure Scan is the “always-on safety net” for client sites. It expands AlmaSEO beyond content into reliability and security, and gives agencies a concrete monitoring story with daily scans, explainable scoring, and alert-driven workflows.

## Overview

Sub-tabs included:
- Scan Overview: health score, detected systems, issues, recommendations, alerts, expiry banners, and scan timeline.
- Domains & DNS: registrar/DNS provider, nameservers, and record-level details (A/CNAME/MX/NS).
- Hosting: hosting provider detection, server/IP details, and plan-level notes where available.
- SSL & Security: certificate validity/issuer/expiry plus security header coverage (HSTS, CSP, etc.).
- Email Providers: email provider discovery, MX records, and SPF/DKIM/DMARC status.

Automation + alerts:
- Manual Scan Now is rate-limited (1/min).
- Background scheduler runs hourly and scans any site not scanned in >24h (batched).
- Alerts are generated from scan conditions and auto-resolve when fixed; critical and digest notifications can be sent via SendGrid based on per-site flags.

AI audit (manual scans):
- When audit=1, generates an infrastructure audit report with sub-scores and HTML output saved to infrastructure_ai_reports.

## Why It Matters

Automates ongoing monitoring of the technical foundation of a client’s site (DNS, hosting, SSL, email auth, security headers), with alerts and AI audits that help teams catch issues early and prioritize fixes.

## Sub-features

- **[Scan Overview](scan-overview.md)** *(Pro)* — Infrastructure Scan child tab that summarizes the site’s current infrastructure health, detected systems, issues, recommendations, and active alert...
- **[Domain & DNS](domain-dns.md)** *(Pro)* — Infrastructure Scan sub-tab for managing domain registration and DNS configuration. Combines manual CRUD records with scan-detected DNS/nameserver ...
- **[Hosting](hosting.md)** *(Pro)* — Infrastructure Scan sub-tab for tracking hosting provider and server details. Combines manual CRUD records with scan-detected hosting/IP discovery....
- **[SSL & Security](ssl-security.md)** *(Pro)* — Infrastructure Scan sub-tab for managing SSL certificate records for the client site. Focuses on certificate inventory and lifecycle management, wh...
- **[Email Providers](email-providers.md)** *(Pro)* — Infrastructure Scan sub-tab for tracking email hosting and authentication configuration. Combines manual CRUD records with scan-detected email/DNS ...

