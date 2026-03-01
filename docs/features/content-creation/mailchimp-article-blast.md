# Mailchimp Article Blast

**Tier:** Pro | **Status:** Shipped | **Type:** Integration

!!! tip "Key Insight"
    Extends AlmaSEO beyond content creation into content distribution. "Create, publish, AND promote — without leaving the dashboard." This closes the loop for users who want a true all-in-one workflow. Currently Mailchimp-only; the per-site credential architecture supports adding other providers (ConvertKit, Klaviyo, etc.) in the future if needed.

## Overview

Send a branded email campaign to Mailchimp subscribers directly from the **Post Details** page after an article is published. The campaign includes a responsive HTML email template with the site's brand colors, logo, featured image (pulled from WordPress), an AI-generated subject line and teaser excerpt, and a "Read Full Article" call-to-action button linking back to the post.

### How It Works

1. **Connect** — Enter Mailchimp API key, from name, reply-to email, and select a default audience list in **Client Profile > Mailchimp** tab. Test the connection before saving.
2. **Compose** — From a published post's detail page, click "Send Email Campaign" to open the campaign modal. Click "Generate AI Subject & Excerpt" to auto-generate a polished subject line (max 60 characters) and a 1-2 paragraph teaser. Both are fully editable.
3. **Preview** — The modal shows a live preview of the email template with your brand colors, logo, featured image, subject, and excerpt.
4. **Send or Draft** — Choose "Save as Draft in Mailchimp" (recommended default) to review and test in Mailchimp before sending, or "Send Immediately" with a confirmation warning.

### Email Template

The email template is built into AlmaSEO — no Mailchimp template setup required. It includes:

- **Header** — Gradient banner using the site's primary and secondary brand colors, with site logo centered above the site name
- **Featured Image** — Pulled automatically from the WordPress post via REST API
- **Article Title** — Centered below the header
- **Teaser Excerpt** — AI-generated or manually written, 1-2 paragraphs
- **CTA Button** — "Read Full Article" styled with the site's primary brand color
- **Footer** — Unsubscribe and update preferences links (Mailchimp merge tags)

### Mailchimp Settings (Client Profile)

Located under **Client Profile > Mailchimp** tab:

- API Key (with visibility toggle)
- From Name (defaults to site name)
- Reply-to Email
- Default Audience List (auto-loaded after connection test)
- Test Connection button with status indicator
- Disconnect option to remove credentials

## Why It Matters

Turns AlmaSEO into a complete content marketing workflow: create an article, publish to WordPress, and blast it to email subscribers — all from the same dashboard. No need to switch to Mailchimp to manually build a campaign.

## Requirements

- **Integrations:** Mailchimp API (v3.0)
- **Compatibility:** WordPress (for featured image retrieval), Static Export sites (without featured image)
- **AI:** OpenAI GPT-4o-mini (for subject line and excerpt generation)

## Target Audience

Agencies, Solo Practitioners, Small Businesses
