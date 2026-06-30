---
title: "Billing & Invoicing"
slug: "billing-invoicing"
type: "feature"
status: "complete"
tier: "Agency"
feature_id: ""
last_updated: "2026-06-30"
---

# Billing & Invoicing

**Tier:** Agency | **Type:** User-Facing UI

!!! tip "Key Insight"
    Billing & Invoicing is a full accounts-receivable system built into AlmaSEO. It handles the entire lifecycle — from creating an invoice, to scheduling it for a future date, to automatically sending reminders when payment is late, to charging a saved card, to applying late fees. Agencies no longer need a separate invoicing tool.

## Overview

Create, schedule, send, and track branded invoices with Stripe payment acceptance. Supports one-time and recurring billing, client-facing autopay, configurable payment reminders, and automatic late fees. The billing page lives at `/billing` and is accessible from the main sidebar navigation.

## Why It Matters

Agencies need to invoice clients, track payments, and follow up on overdue balances. Without a built-in system, this means juggling QuickBooks, Stripe dashboards, and manual email follow-ups. Billing & Invoicing consolidates all of that into the same platform where work is tracked, eliminating context-switching and ensuring invoices reflect actual work performed.

## What It Does

### Invoice Management

- Create invoices with line items, tax rates, discounts, notes, and custom footer text
- Assign invoices to billing clients (managed in the Clients tab)
- Set issue date and due date independently
- Invoices support statuses: **Draft**, **Scheduled**, **Sent**, **Paid**, **Overdue**, **Void**
- Edit draft and scheduled invoices before they go out
- Void unpaid invoices at any time
- Copy shareable payment links for any invoice

### Scheduled Sending

When the issue date is set to a future date, clicking "Save & Send" automatically schedules the invoice instead of sending it immediately. The button label changes dynamically to "Save & Schedule (date)" to make this clear.

- Scheduled invoices appear with an amber **scheduled** badge in the invoice list
- A daily job at **8:05 AM** checks for scheduled invoices whose issue date has arrived and sends them automatically
- Scheduled invoices can be sent early using the "Send Now" button, or edited before they go out

### Recurring Invoices

Mark any invoice as recurring to have it automatically regenerated on a set schedule.

- **Frequencies:** Weekly, Biweekly, Monthly, Quarterly, Annually
- **Optional end date** — leave blank for indefinite recurrence
- **Auto-send** — new recurring invoices are emailed to the client automatically
- A daily job at **8:15 AM** generates new invoices from recurring templates whose next recurrence date has arrived
- Each generated invoice is a full copy (line items, tax, discount, notes) with updated dates

### Client-Facing Autopay

Clients can opt into autopay directly from the public invoice payment page.

- Recurring invoices show an "Enable Autopay" card on the payment page (`/pay/<token>`)
- Clicking "Set up autopay" redirects the client to Stripe Checkout in setup mode to save a card
- Once a card is saved, the client record is updated with `autopay_enabled = true`
- Future recurring invoices are automatically charged against the saved card — no client action needed
- The invoice creation form shows a read-only indicator: "Client has autopay enabled" or "No autopay"
- The invoice email template includes an autopay section for recurring invoices (opt-in CTA or confirmation)

### Payment Reminders

Configurable automatic reminder emails sent to clients based on invoice due dates.

- **Default schedule:** 3 days before due, on due date, 7 days overdue, 14 days overdue
- Each reminder tier has escalating tone and a color-coded status badge:
    - **Upcoming (blue):** Friendly heads-up
    - **Due today (yellow):** Urgent notice
    - **Overdue (red):** Past-due warning with stronger language
- Runs daily at **9:00 AM**
- Only one reminder per invoice per day (tracked via `last_reminder_at`)
- Invoices are auto-marked as "overdue" when past due
- You receive a BCC copy of every reminder if "Send me a copy" is enabled in settings
- Configurable per user — toggle the whole system on/off and pick which intervals are active

### Late Fees

Optional automatic late fee applied to overdue invoices after a configurable grace period.

- **Off by default** — must be enabled in billing settings
- **Fee types:** Flat amount (e.g., $25) or percentage of invoice total (e.g., 1.5%)
- **Grace period:** Configurable (default: 15 days after due date)
- When triggered, a late fee line item is added to the invoice (e.g., "Late fee (flat — 22 days past due)")
- Invoice totals are recalculated including tax on the new subtotal
- Client receives a branded "Late fee applied" email with the fee breakdown and new balance
- **One-time only** — the system will not stack multiple late fees on the same invoice
- Runs daily at **9:15 AM**

### Stripe Integration

- Clients pay via Stripe Checkout from the public payment page
- Supports Visa, Mastercard, Amex, Discover, and bank transfers
- Stripe webhook (`checkout.session.completed`) automatically marks invoices as paid — no manual action needed
- Supports Stripe Connect for agencies with their own Stripe accounts
- Manual "Record Payment" button available for offline payments (check, wire, cash)

### Invoice Emails

Every invoice email includes:

- Business logo (if uploaded)
- "Your invoice is ready" hero with balance due and due date
- Two "View and pay" CTA buttons (top and bottom)
- Payment method badges (Visa, MC, Amex, Disc, Bank)
- Full line item table with subtotal, discount, tax, and total
- Personal note (if added in the invoice builder)
- Footer note (from billing settings default)
- Autopay section for recurring invoices (opt-in CTA or confirmation badge)
- PDF attachment of the invoice
- BCC copy to the agency owner (if enabled)

### Billing Settings

Accessible via the gear icon on the billing page:

| Setting | Description |
|---------|-------------|
| **Business / Agency Name** | Shown on invoices and emails |
| **Reply-To / Contact Email** | Client replies go here. Also used as BCC address for invoice copies |
| **Phone** | Shown in invoice footer |
| **Invoice Prefix** | Prefix for invoice numbers (e.g., ALM-001) |
| **Business Address** | Shown in invoice and email footer |
| **Default Due Days** | Default number of days until payment is due |
| **Default Tax Rate** | Auto-applied tax percentage |
| **Default Invoice Footer** | Boilerplate text at the bottom of every invoice |
| **Send me a copy** | BCC every invoice and reminder email to your reply-to email |
| **Auto-send payment reminders** | Toggle + interval checkboxes (3d before, due date, 7d late, 14d late) |
| **Charge late fees** | Toggle + fee type (flat/percentage), amount, and grace period |

### Billing Clients

The Clients tab manages the contact records used for invoicing:

- Client name, company name, email, phone, address
- Stripe customer ID (auto-created on first payment)
- Autopay status and saved payment method
- Import clients from existing AlmaSEO sites
- Archive inactive clients

## How to Use It

### Creating and Sending an Invoice

1. Go to the **Billing** page from the sidebar.
2. Click **New Invoice**.
3. Select a client (or add one if none exist).
4. Add line items with description, quantity, and rate.
5. Set the issue date and due date.
6. Optionally add a personal note.
7. Click **Save & Send** to send immediately, or set a future issue date to schedule it.
8. The client receives a branded email with a "View and pay" link.

### Setting Up Recurring Billing

1. When creating an invoice, check **Make this a recurring invoice**.
2. Choose a frequency (monthly, quarterly, etc.) and optionally set an end date.
3. Check **Auto-send to client** to have recurring invoices emailed automatically.
4. Save the invoice. Future invoices will be generated and sent on schedule.

### Configuring Reminders and Late Fees

1. Click the **gear icon** on the billing page to open settings.
2. Under **Auto-send payment reminders**, toggle on and select which intervals you want.
3. Under **Charge late fees**, toggle on, choose flat or percentage, set the amount and grace period.
4. Click **Save Settings**.

## Automated Schedule

| Time | Job | Description |
|------|-----|-------------|
| 8:05 AM | Scheduled invoice sender | Sends invoices with status "scheduled" whose issue date has arrived |
| 8:15 AM | Recurring invoice processor | Generates new invoices from recurring templates due today |
| 9:00 AM | Payment reminders | Sends reminder emails based on each user's configured schedule |
| 9:15 AM | Late fee processor | Applies late fees to overdue invoices past the grace period |

## Technical Details

### Key Files

| File | Purpose |
|------|---------|
| `routes/billing_routes.py` | All billing API endpoints, email templates, processors |
| `templates/billing.html` | Billing dashboard UI (invoices, clients, settings, expenses) |
| `templates/billing_pay.html` | Public invoice payment page |
| `utils/invoice_pdf.py` | PDF invoice generation |
| `dashboard.py` | Scheduler job registration |

### Database Tables

| Table | Purpose |
|-------|---------|
| `invoices` | Invoice records with status, dates, amounts, recurring config, reminder tracking, late fee tracking |
| `invoice_items` | Line items for each invoice |
| `billing_clients` | Client contact records with Stripe and autopay info |
| `billing_settings` | Per-user business info, defaults, reminder config, late fee config |
| `expenses` | Expense tracking (separate from invoicing) |

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/billing/invoices` | List invoices (filterable by status) |
| POST | `/api/billing/invoices` | Create invoice |
| GET | `/api/billing/invoices/<id>` | Invoice detail with line items |
| PUT | `/api/billing/invoices/<id>` | Update invoice |
| POST | `/api/billing/invoices/<id>/send` | Send invoice email |
| POST | `/api/billing/invoices/<id>/record-payment` | Record manual payment |
| POST | `/api/billing/invoices/<id>/void` | Void invoice |
| GET | `/api/billing/clients` | List billing clients |
| POST | `/api/billing/clients` | Create client |
| PUT | `/api/billing/clients/<id>` | Update client |
| GET/POST | `/api/billing/settings` | Get/update billing settings |
| GET | `/api/billing/revenue-summary` | Revenue overview |
| GET | `/pay/<token>` | Public invoice payment page |
| POST | `/pay/<token>/checkout` | Create Stripe checkout session |
| POST | `/pay/<token>/setup-autopay` | Client-facing autopay card save |
| POST | `/api/billing/payment-webhook` | Stripe webhook for payment events |
