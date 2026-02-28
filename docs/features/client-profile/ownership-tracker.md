# Ownership Tracker

**Tier:** Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    A practical agency retention feature: once the Ownership Tracker is populated, AlmaSEO becomes the operational home for the account. The lock overlay + optional password lets teams choose between convenience and security, while the structured tabs make it hard to forget critical services like DNS, SSL, renewals, and payment processors.

## Overview

Lock screen + password protection:
- First visit shows a lock overlay with branded background.
- Set optional password (min 6 chars), hashed with werkzeug.
- Skip to use unprotected.
- Unlock on subsequent visits (session-based).
- Forgot password sends email reset link (token expires in 1 hour).
- Change password from inside unlocked view (verifies current password).

Spreadsheet (unlocked):
- Multi-sheet workbook with 13 pre-configured tabs: Company Information, Domain Registration, Website Hosting, DNS Management, Website CMS/Platform, Email Hosting, SSL Certificate, Analytics & Marketing, Backup Information, Development & Support, Payment Processors, Additional Services, Renewal Calendar.
- Each sheet uses 3 columns: Item | Value | Notes, pre-populated with example/placeholder rows.

Spreadsheet capabilities:
- Editing: add/delete rows and columns, right-click context menu, drag rows/columns, undo/redo.
- Formatting toolbar: bold/italic/underline/strikethrough, text + background colors, alignment, clear formatting.
- Sheet management: add/rename/delete (cannot delete last sheet), reorder tabs via drag-and-drop.
- Persistence: Save button stores all sheets JSON to ownership_tracker table, shows “last saved” timestamp, and warns on page leave if unsaved changes exist (beforeunload).

## Why It Matters

Gives agencies and clients a single secure place to store and maintain the “keys to the kingdom” for a site, reducing onboarding friction and preventing credential loss.

## Access Control

**Permission Mode:** Fixed

