---
title: "AlmaSEO WordPress Connector Plugin"
slug: "almaseo-wordpress-connector-plugin"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "PL-WP-CONNECTOR"
last_updated: "2026-03-15"
---

# AlmaSEO WordPress Connector Plugin

## Overview

The AlmaSEO WordPress Connector Plugin is a lightweight WordPress plugin that acts as a secure bridge between a WordPress site and the AlmaSEO platform. It enables two-way communication so AlmaSEO can publish content, manage SEO metadata, detect installed SEO plugins, and run optimization workflows on the connected site — all without requiring manual copy/paste or direct WordPress admin access.

The Connector is the **foundation of the WordPress integration**. Every WordPress-dependent feature — content publishing, metadata syncing, schema injection, and automation — requires the Connector (or its upgraded counterpart, the SEO Playground) to be installed and active.

**Current Version:** 2.1.4

---

## What It Does

### Secure Authentication

The Connector supports two authentication methods, automatically selecting the right one for each hosting environment:

**Method 1 — Application Passwords (Basic Auth)**

The standard WordPress authentication method, available since WordPress 5.6. The plugin generates an Application Password and AlmaSEO uses it with Basic Auth (`Authorization: Basic`) on every API request.

**Method 2 — JWT Token Authentication**

Some hosting providers (GoDaddy, SiteGround, Bluehost, and others) run server-level firewalls (WAFs) that strip the `Authorization` header from REST API requests, which breaks Application Passwords entirely. For these hosts, the Connector provides JWT (JSON Web Token) authentication as a built-in alternative.

- The plugin generates a **64-character HMAC secret** on activation, stored in `almaseo_jwt_secret`.
- A signed **HS256 JWT token** is created containing the username, site URL, issue time, and a 365-day expiry.
- The token is passed via a custom **`X-AlmaSEO-Token` header** — custom headers are not stripped by hosting WAFs, unlike the `Authorization` header.
- The plugin validates the signature, expiry, scope, and user permissions on every request.

Both methods are available simultaneously — the plugin checks for JWT first, then falls back to Basic Auth. The AlmaSEO dashboard auto-detects which format was entered and routes accordingly.

**Connection setup paths:**

- **Auto-connect** — a secret-based flow where the plugin generates and returns credentials automatically, requiring minimal user effort.
- **Manual setup** — the user copies their Application Password or JWT Token from the plugin settings and enters it into AlmaSEO.
- **Smart fallback** — if Application Password generation fails (due to hosting restrictions), the plugin automatically detects the block and presents the JWT Token as the recommended connection method.

A 32-character shared secret is generated on plugin activation and validated using `hash_equals()` for timing-attack resistance. CORS headers restrict API access to `https://api.almaseo.com` only.

### SEO Metadata Writing

The Connector writes SEO metadata from AlmaSEO directly into the fields used by the site's active SEO plugin. This includes:

- SEO title and meta description
- Focus keywords
- Open Graph tags (title, description)
- Twitter Card tags (title, description)
- Canonical URLs
- Robots directives
- Schema markup (on supported plugins)

**Supported SEO plugins:**

| Plugin | Write Method |
|--------|-------------|
| All in One SEO (AIOSEO) | AIOSEO internal API, direct database, or post meta fallback |
| Yoast SEO | Post meta |
| Rank Math | Post meta |
| SEOPress | Post meta |
| The SEO Framework | Post meta |

The Connector auto-detects which SEO plugin is installed and selects the correct write method. For AIOSEO, it tries three approaches in order (internal API → database → post meta) to handle both Free and Pro versions.

### SEO Plugin Detection

The Connector reports back to AlmaSEO which SEO plugin is active on the WordPress site, including:

- Plugin name and version
- Whether it's a Free or Pro edition
- What capabilities it supports (metadata writing, schema, REST API access)

This allows AlmaSEO to adapt its behavior per site — writing metadata to the correct fields and showing relevant warnings if a plugin's configuration is incomplete.

### Site Capabilities Reporting

An endpoint exposes what the WordPress site supports, including:

- Available post types (posts, pages, custom types)
- Available taxonomies (categories, tags, custom taxonomies)
- REST API availability
- Application Password support
- Custom field support

### Connection Verification

AlmaSEO can check the health of the connection at any time, confirming:

- The plugin is installed and active
- The plugin version
- Site information (name, URL, WordPress version)
- Whether credentials are valid or stale

### Plugin State Detection

AlmaSEO tracks the state of AlmaSEO plugins on each connected site:

| State | Meaning |
|-------|---------|
| `none` | No AlmaSEO plugin detected |
| `connector_only` | Connector is active |
| `playground_only` | SEO Playground is active (ideal) |
| `both` | Both plugins active (conflict — user must deactivate Connector) |
| `installed_not_active` | Plugin found but not activated |
| `error` | Site unreachable or REST API disabled |

---

## Why It Matters

- **Unlocks the entire WordPress workflow** — without the Connector, AlmaSEO cannot publish content, write SEO metadata, or manage a WordPress site. It's the single dependency for all WordPress-related features.
- **Zero manual metadata entry** — SEO titles, descriptions, Open Graph tags, and schema are pushed directly into the correct plugin fields. No logging into WordPress to copy/paste.
- **Works with your existing SEO plugin** — supports AIOSEO, Yoast, Rank Math, SEOPress, and The SEO Framework. No need to switch plugins.
- **Auto-detection, not configuration** — the Connector figures out what's installed and adapts. Users don't need to know the technical details.
- **Secure by design** — secret-based authentication, CORS restrictions, nonce verification, admin-only permission checks, and timing-safe comparisons. No credentials are exposed in transit.
- **Lightweight** — the Connector is a small plugin (~1 MB) that adds no admin bloat. It does the bridge work and stays out of the way.

---

## How to Use It

### Step 1: Download the Plugin

1. Open a site's **Client Profile** in AlmaSEO.
2. Navigate to the **AlmaSEO for WordPress** tab.
3. Click **Download Connector**.
4. The plugin ZIP file downloads to your computer.

### Step 2: Install on WordPress

1. Log into your WordPress admin dashboard.
2. Go to **Plugins → Add New → Upload Plugin**.
3. Select the downloaded ZIP file.
4. Click **Install Now**, then **Activate**.

On activation, the plugin:

- Generates a shared secret for secure communication
- Generates a JWT signing secret for alternative authentication
- Redirects to the **AlmaSEO Connector** settings page
- Appears as a top-level item in the WordPress admin sidebar

### Step 3: Connect to AlmaSEO

**Option A — Auto-Connect (Recommended):**

1. Back in AlmaSEO, the plugin status should update to show the Connector is detected.
2. Follow the auto-connect prompts — AlmaSEO passes a secret to the plugin, which returns credentials automatically.
3. Connection is established with no manual credential entry.

**Option B — Application Password (Standard Hosts):**

1. In WordPress, go to **Users → Your Profile → Application Passwords**.
2. Enter a name (e.g., "AlmaSEO") and click **Add New Application Password**.
3. Copy the generated password.
4. In AlmaSEO, go to the site's connection screen or **WordPress Settings** tab.
5. Enter your WordPress username and paste the Application Password into the **Authentication Token** field.
6. Click **Connect** or **Test Connection** to verify.

**Option C — JWT Token (Restricted Hosts):**

If your hosting provider blocks Application Passwords (common on GoDaddy, SiteGround, Bluehost, and other managed hosts), the plugin will detect the issue automatically when you click **Generate Password** and present the JWT Token as the recommended alternative:

1. In WordPress admin, go to **AlmaSEO Connector** in the sidebar.
2. Click **Generate Password** — the plugin tests whether Application Passwords work on your host.
3. If blocked, the plugin shows a **"Use JWT Token Instead"** section with the token ready to copy.
4. Copy the **JWT Token**.
5. In AlmaSEO, paste the JWT Token into the **Authentication Token** field. The dashboard auto-detects the format — no need to specify that it's a JWT.
6. Click **Connect** to verify.

!!! note "The Authentication Token field accepts both formats"
    You can paste either an Application Password or a JWT Token into the same field. AlmaSEO detects which type it is automatically. WordPress username is optional when using JWT.

### Step 4: Verify the Connection

1. In the **AlmaSEO for WordPress** tab, confirm the status shows the plugin as active with the correct version.
2. In the **WordPress SEO Plugin** tab, confirm the detected SEO plugin is correct.
3. Optionally, click **Check Plugin Health** to verify metadata writing and schema support.

---

## Key Settings / Options

### Plugin Status & Detection

| Setting | Location | Description |
|---------|----------|-------------|
| Plugin state | AlmaSEO for WordPress tab | Shows current detection state (connector_only, playground_only, both, none, error) |
| Plugin version | AlmaSEO for WordPress tab | Version of the active AlmaSEO plugin |
| Outdated warning | AlmaSEO for WordPress tab | Alert when a newer version is available |
| Cached check | Automatic | Plugin status is cached for fast page loads; refresh to force a new check |

### WordPress Connection

| Setting | Location | Description |
|---------|----------|-------------|
| WordPress username | WordPress Settings tab | The WordPress admin username (optional for JWT) |
| Application Password | WordPress Settings tab | The Application Password for Basic Auth (show/hide toggle) |
| JWT Token | WordPress Settings tab | Alternative authentication token for hosts that block Application Passwords. Shows Active/Expiring Soon/Expired badge |
| Connection status | WordPress Settings tab | Badge showing connected, error, or unknown. Shows "(JWT)" when connected via JWT |
| JWT expiry warning | WordPress Settings tab & Overview tab | Red alert if token has expired, yellow alert if expiring within 30 days, with step-by-step renewal instructions |
| Test Connection | WordPress Settings tab | Button to verify credentials are valid. Auto-suggests JWT if Basic Auth is blocked with 403 |

### SEO Plugin Configuration

| Setting | Location | Description |
|---------|----------|-------------|
| Detected SEO plugin | WordPress SEO Plugin tab | Auto-detected from the WordPress site |
| SEO plugin override | WordPress SEO Plugin tab | Dropdown to manually select a different SEO plugin |
| Plugin health check | WordPress SEO Plugin tab | Tests API access, metadata writing, and schema support |

### Security

| Setting | Value | Description |
|---------|-------|-------------|
| CORS origin | `https://api.almaseo.com` | Only AlmaSEO can call plugin endpoints |
| Shared secret | Auto-generated (32 chars) | Protects auto-connect and password generation endpoints |
| Secret source | `wp_options` or `wp-config.php` | `ALMASEO_SECRET` constant in wp-config takes priority |
| JWT signing secret | Auto-generated (64 chars) | Stored in `almaseo_jwt_secret` option, used for HS256 token signing |
| JWT token expiry | 365 days | Tokens expire after one year; dashboard shows warnings starting 30 days before |
| JWT delivery | `X-AlmaSEO-Token` header | Custom header bypasses WAF restrictions on `Authorization` |
| Nonce verification | WordPress standard | Required for admin-only operations |

### Connector vs SEO Playground

| Aspect | Connector (v2.1.4) | SEO Playground (v8.7.0) |
|--------|---------------------|-------------------------|
| Purpose | Bridge only | Bridge + full SEO toolkit |
| Size | ~350 KB | ~5-10 MB |
| Authentication | Application Passwords + JWT | Application Passwords + JWT |
| Admin UI | Settings page only | Full admin pages and meta boxes |
| SEO editing | None | Bulk meta editor, schema, health scoring, and more |
| Upgrade path | Deactivate Connector → install Playground | N/A |
| Conflict | Cannot run alongside Playground | Cannot run alongside Connector |

If both plugins are detected as active, AlmaSEO shows a conflict warning and instructs the user to deactivate the Connector.

---

## Notes / Edge Cases

- **Application Passwords blocked by hosting** — some hosting providers (GoDaddy, SiteGround, Bluehost, and similar managed hosts) strip the `Authorization` header from REST API requests via their server-level WAF/ModSecurity rules. This breaks Application Passwords entirely. The Connector detects this automatically when the user clicks "Generate Password" — the password is created and immediately tested via REST API. If the test fails, the plugin shows the JWT Token as the recommended alternative. Manual Application Password creation through Users → Profile will also fail on these hosts for the same reason.
- **JWT token expiry** — JWT tokens expire after 365 days. The AlmaSEO dashboard reads the expiry directly from the token's payload (no database tracking needed) and shows warnings starting 30 days before expiry. When expired, a red alert with step-by-step renewal instructions appears on both the Overview and WordPress Settings tabs.
- **JWT token renewal** — to renew an expiring or expired token, visit the AlmaSEO Connector settings page in WordPress admin. A fresh token is generated each time the page loads. Copy it and paste it into the WordPress Settings tab in AlmaSEO.
- **Authentication auto-detection** — the AlmaSEO dashboard's Authentication Token field accepts both Application Passwords and JWT Tokens. The format is detected automatically (JWT tokens have three dot-separated segments starting with "eyJ"). No separate field or manual selection is needed.
- **AIOSEO Pro without REST API** — if AIOSEO Pro's REST API addon is not enabled, the Connector falls back to direct database writes or post meta. A specific warning is shown in the health check.
- **Stale credentials** — if an Application Password is revoked in WordPress, the connection will fail with a 401 error. The user must generate a new password and update it in AlmaSEO.
- **REST API disabled** — if the WordPress REST API is disabled (by a security plugin or server config), the Connector cannot function. The plugin state will show as `error`. Note: JWT authentication still requires the REST API to be accessible — it only bypasses the `Authorization` header restriction, not the REST API itself.
- **Activity logging** — plugin downloads, state changes, connection tests, and metadata updates are logged to the site's Activity & Logs timeline.
- **Credential storage** — credentials are stored in the AlmaSEO database (`sites` table). JWT tokens are stored in the `almaseo_token` column; Application Passwords are stored in `wp_app_password`. The system checks `almaseo_token` first. Both are marked as sensitive and excluded from debug logs.

### Sub-features

- **[SEO Playground (WordPress On-Site SEO Toolkit)](seo-playground.md)** — The upgraded plugin that includes all Connector capabilities plus a complete on-site SEO management suite. Available as a separate install for users who want the full WordPress SEO toolkit.
