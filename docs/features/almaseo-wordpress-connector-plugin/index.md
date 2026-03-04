---
title: "AlmaSEO WordPress Connector Plugin"
slug: "almaseo-wordpress-connector-plugin"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "PL-WP-CONNECTOR"
last_updated: "2026-03-04"
---

# AlmaSEO WordPress Connector Plugin

## Overview

The AlmaSEO WordPress Connector Plugin is a lightweight WordPress plugin that acts as a secure bridge between a WordPress site and the AlmaSEO platform. It enables two-way communication so AlmaSEO can publish content, manage SEO metadata, detect installed SEO plugins, and run optimization workflows on the connected site — all without requiring manual copy/paste or direct WordPress admin access.

The Connector is the **foundation of the WordPress integration**. Every WordPress-dependent feature — content publishing, metadata syncing, schema injection, and automation — requires the Connector (or its upgraded counterpart, the SEO Playground) to be installed and active.

**Current Version:** 1.5.0

---

## What It Does

### Secure Authentication

The Connector establishes a secure connection between WordPress and AlmaSEO using WordPress Application Passwords (Basic Auth). It supports two setup paths:

- **Auto-connect** — a secret-based flow where the plugin generates and returns credentials automatically, requiring minimal user effort.
- **Manual setup** — the user generates an Application Password in WordPress and enters it into AlmaSEO.

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
3. Click **Download Connector v1.5.0**.
4. The plugin ZIP file downloads to your computer.

### Step 2: Install on WordPress

1. Log into your WordPress admin dashboard.
2. Go to **Plugins → Add New → Upload Plugin**.
3. Select the downloaded `alma-seoconnector-v1.5.0.zip` file.
4. Click **Install Now**, then **Activate**.

On activation, the plugin automatically generates a shared secret for secure communication.

### Step 3: Connect to AlmaSEO

**Option A — Auto-Connect (Recommended):**

1. Back in AlmaSEO, the plugin status should update to show the Connector is detected.
2. Follow the auto-connect prompts — AlmaSEO passes a secret to the plugin, which returns credentials automatically.
3. Connection is established with no manual credential entry.

**Option B — Manual Setup:**

1. In WordPress, go to **Users → Your Profile → Application Passwords**.
2. Enter a name (e.g., "AlmaSEO") and click **Add New Application Password**.
3. Copy the generated password.
4. In AlmaSEO, go to the site's **Client Profile → WordPress Settings** tab.
5. Enter your WordPress username and the Application Password.
6. Click **Test Connection** to verify.

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
| WordPress username | WordPress Settings tab | The WordPress admin username used for API access |
| Application Password | WordPress Settings tab | The Application Password for Basic Auth (show/hide toggle) |
| Connection status | WordPress Settings tab | Badge showing connected, error, or unknown |
| Test Connection | WordPress Settings tab | Button to verify credentials are valid |

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
| Nonce verification | WordPress standard | Required for admin-only operations |

### Connector vs SEO Playground

| Aspect | Connector (v1.5.0) | SEO Playground (v7.9.0) |
|--------|---------------------|-------------------------|
| Purpose | Bridge only | Bridge + full SEO toolkit |
| Size | ~1 MB | ~5-10 MB |
| Admin UI | Settings page only | Full admin pages and meta boxes |
| SEO editing | None | Bulk meta editor, schema, health scoring, and more |
| Upgrade path | Deactivate Connector → install Playground | N/A |
| Conflict | Cannot run alongside Playground | Cannot run alongside Connector |

If both plugins are detected as active, AlmaSEO shows a conflict warning and instructs the user to deactivate the Connector.

---

## Notes / Edge Cases

- **Application Password support** — requires WordPress 5.6+. Some managed hosting providers (e.g., GoDaddy Managed WordPress) may restrict Application Password generation.
- **AIOSEO Pro without REST API** — if AIOSEO Pro's REST API addon is not enabled, the Connector falls back to direct database writes or post meta. A specific warning is shown in the health check.
- **Stale credentials** — if an Application Password is revoked in WordPress, the connection will fail with a 401 error. The user must generate a new password and update it in AlmaSEO.
- **REST API disabled** — if the WordPress REST API is disabled (by a security plugin or server config), the Connector cannot function. The plugin state will show as `error`.
- **Activity logging** — plugin downloads, state changes, connection tests, and metadata updates are logged to the site's Activity & Logs timeline.
- **Credential storage** — Application Passwords are stored in the AlmaSEO database (`sites` table). The auto-connect flow stores them in `almaseo_token`; manual entry stores them in `wp_app_password`. The system checks `almaseo_token` first.

### Sub-features

- **[SEO Playground (WordPress On-Site SEO Toolkit)](seo-playground.md)** — The upgraded plugin that includes all Connector capabilities plus a complete on-site SEO management suite. Available as a separate install for users who want the full WordPress SEO toolkit.
