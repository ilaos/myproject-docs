# Scan Overview

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    This tab turns “infrastructure” into a product loop: daily scans surface issues, alerts drive action, and the scan timeline + AI audit create an explainable history of risk and remediation. It also provides a clean navigation hub into the more detailed DNS/hosting/SSL/email sub-tabs.

## Overview

What each scan checks (real network checks):
- SSL/TLS: certificate validity, issuer, expiration.
- Security headers: HSTS, X-Content-Type-Options, X-Frame-Options, CSP, X-XSS-Protection.
- DNS: A/CNAME/MX/NS records and nameserver detection.
- IP & hosting: IP resolution and hosting provider fingerprinting (AWS, GCP, DigitalOcean, etc.).
- Email auth: SPF/DKIM/DMARC validation.
- CMS: platform fingerprinting (WordPress, Drupal, Joomla, etc.).
- CDN: Cloudflare/Akamai/Fastly detection.
- Analytics: GA4/GTM detection (static + runtime via Playwright headless browser).
- Performance: HTTP response time.

Returns a health score (0–100) based on deductions for issues found.

UI sections:
- Health Score Card: circular score (0–100), risk badge (Low/Medium/High/Critical), last audit timestamp, issue counts by severity.
- Detected Systems Grid (6 cards): DNS & nameservers, hosting provider & location, SSL status & expiry, email auth status, CMS platform & version, analytics & CDN status.
- Smart Actions Bar: priority-sorted recommendation chips that deep-link into relevant sections (e.g., Fix SSL, Add SPF, Configure DKIM, Consider CDN).
- Issues Panel: problems sorted by severity.
- Recommendations Panel: AI-generated and/or rule-based suggestions.
- Alerts: bell icon with badge count and dropdown, plus link to full alert drawer; alerts can be individually resolved.
- Expiry Alert Banner: critical expirations (<7 days).
- Scan Timeline: history of past scans with ability to inspect previous scan details.

Scan triggers:
- Manual: Scan Now button (rate-limited to 1 scan per 60 seconds).
- Automatic: hourly scheduler scans any site with last scan >24 hours ago (batches up to 5 sites per cycle, 5-second delay between scans).

AI audit (manual scan sets audit=1):
- Generates GPT-4 infrastructure audit report with overall + sub-scores (security, performance, reliability), plus critical issues, warnings, suggestions, and full HTML report.
- Saved to infrastructure_ai_reports table.

Alert system:
- Alerts are auto-generated from scan results (critical/warning/info) and auto-resolve when fixed on subsequent scans.
- Email notifications via SendGrid: critical alerts immediately; optional daily digest of unresolved alerts (per-site flags infra_notify_critical and infra_notify_digest).

## Why It Matters

Gives a clear, single-screen infrastructure health snapshot with prioritized actions and alerts, so issues like expiring SSL, broken email auth, or missing security headers get caught and fixed before they impact rankings or deliverability.

