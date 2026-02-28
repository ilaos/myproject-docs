# AI Review Response Drafting

**Tier:** Pro | **Type:** User-Facing UI

!!! tip "Key Insight"
    Simple but high leverage: turns GBP reputation management into a fast workflow inside AlmaSEO. The rating-based tone and guardrails reduce risky AI behavior, while regenerate + editable draft keeps the user in control.

## Overview

- Reviews without an owner reply show a “Draft Reply” button.
- Reviews with an existing reply show a “Redraft Reply” button.
- Clicking generates a draft reply (spinner → result) and renders an editable textarea.
- Actions: Copy to Clipboard, Regenerate.

Tone logic:
- 4–5 stars: grateful, personal, brief.
- 3 stars: appreciative, constructive, invites them back.
- 1–2 stars: empathetic, apologetic, offers resolution, never defensive.

Prompt guardrails:
- Uses the customer’s first name.
- 2–4 sentences.
- Never invents specifics not in the review.
- Writes in the business owner’s voice.

Backend:
- POST /api/business-profile/reviews/<site_id>/draft-reply
- Input: { review_text, review_rating, review_author, business_name }
- Output: { success: true, draft_reply }
- Uses GPT-4 (max_tokens=300, temperature=0.7).

Notes:
- Includes a related fix to ensure review text displays correctly (backend returns text field consistently) and adds review_id for identification.

## Why It Matters

Saves time and reduces stress replying to reviews while keeping responses professional, on-brand, and appropriate to the review sentiment.

## Requirements

- **Integrations:** Google API, OpenAI API
- **Depends On:** Business Profile

## Target Audience

Agencies, DIY Business Owners, Freelancers

