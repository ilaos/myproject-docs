# GBP Business Info → NAP Shield Ground Truth

**Tier:** Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    “Ground truth” verification makes NAP Shield more credible: users stop guessing and can validate against Google’s canonical record. It also frames NAP Shield as verification-first (detect → review → decide), which is a strong agency story.

## Overview

Adds a “Google Business Profile Verification” panel inside NAP Shield that fetches Google’s live business info and compares it field-by-field against the user’s master NAP record.

What it does:
- When viewing the NAP Shield master record, the backend checks whether GBP is connected.
- If connected, fetches live GBP location data from the mybusinessbusinessinformation API (readMask includes name/title, storefrontAddress, phoneNumbers, websiteUri).
- Normalizes GBP data into NAP fields (business name, street, city, state, ZIP, phone, website).
- Compares each field case-insensitively against the master NAP.
- Returns additional response fields:
	- gbp_nap: Google’s NAP values
	- gbp_discrepancies: mismatched fields with both values
	- gbp_connected: whether GBP data was available

UI behavior:
- Panel appears only when GBP is connected.
- If all fields match: green “All Match” badge + success alert.
- If mismatches: warning badge (count) + warning alert + comparison table (Your Master NAP vs Google Shows).

Non-goals / constraints:
- Does not auto-update master NAP.
- Does not modify GBP data.
- If GBP fetch fails, panel simply does not show.

Discrepancy detection:
- Flags only when both values exist and differ.
- If either side is blank, it is treated as completeness, not a discrepancy.

## Why It Matters

Gives users immediate, trustworthy confirmation that their master NAP matches what Google shows (or highlights exactly what’s out of sync), improving local SEO reliability and reducing manual checking.

## Requirements

- **Integrations:** Google API
- **Depends On:** Business Profile

## Access Control

**Permission Mode:** Configurable per client

## Target Audience

Agencies, DIY Business Owners, Freelancers

