---
title: "Alma AI Chat"
slug: "alma-ai-chat"
type: "feature"
status: "complete"
last_updated: "2026-03-04"
---

# Alma AI Chat — Global AI Assistant

## Overview

Alma AI Chat is a floating chat assistant available on every page of AlmaSEO. It gives users instant, conversational access to their live platform data — sites, posts, automation jobs, Google Analytics, Google Search Console, SEO audits, and more — without leaving the page they're on.

Alma is powered by GPT-4o-mini with OpenAI function calling. She has access to 18 built-in tools that query real data from your database and connected Google services, and she maintains a persistent conversation history across sessions.

Her persona is **Alma, Director of Operations at AlmaSEO** — a friendly, knowledgeable assistant who oversees content, SEO strategy, automation, and the whole team.

---

## What It Does

### Conversational Data Access

Ask plain-English questions and get answers drawn from your actual data — not generic advice. Alma automatically selects the right tools to answer each question.

**Examples of what you can ask:**

- "What sites do I have?"
- "How is my automation performing?"
- "Show me my recent posts"
- "Why did my last automation job fail?"
- "What content gaps should I focus on?"
- "How is my organic traffic trending this month?"
- "What keywords are driving the most clicks?"
- "Compare my traffic sources with my search performance"

### 18 Built-in Data Tools

Alma can pull live data using the following tools during any conversation:

#### Site & Content

| Tool | What It Returns |
|------|-----------------|
| Get User Sites | All your sites with status and basic info |
| Get Site Details | Full business info, services, location, and settings |
| Get Recent Posts | Posts with topic, status, published date, and word count |
| Get Automation Status | Whether automation is enabled, frequency, schedule, and AI model |
| Get Recent Automation Jobs | Job history with status, timestamps, and error summaries |
| Get Job Error Details | Detailed error log for a specific failed job |

#### SEO & Analysis

| Tool | What It Returns |
|------|-----------------|
| Get SEO Audit Summary | Latest audit metrics — clicks, impressions, CTR, top issues |
| Get Content Gaps | Underperforming keywords and content opportunities from GSC data |
| Get Site Health Overview | Aggregate health — post counts, automation status, last audit, recent errors |
| Get Notifications | Your recent platform notifications |

#### Google Analytics (GA4)

| Tool | What It Returns |
|------|-----------------|
| Get Analytics Overview | Users, sessions, bounce rate, engagement, session duration (up to 90 days) |
| Get Traffic Sources | Channel breakdown — Organic, Direct, Social, Referral — with percentages |
| Get Top Landing Pages | Best-performing pages by sessions with bounce rate and avg duration |
| Get Analytics Trends | Daily sessions and users to spot growth patterns or drops |

#### Google Search Console

| Tool | What It Returns |
|------|-----------------|
| Get Search Performance | Total clicks, impressions, average CTR, and average position (up to 90 days) |
| Get Top Search Queries | Keywords driving traffic with clicks, impressions, CTR, and position (up to 50) |
| Get Top Pages (GSC) | Pages ranked by search clicks with impressions and CTR (up to 50) |
| Get Device Breakdown | Search performance split by desktop, mobile, and tablet |

### Context Awareness

Alma automatically detects which site and page you're currently viewing and uses that as context for her responses. She also knows your username and the current date/time, making answers specific to your situation.

### Conversation History

Chat history persists across browser sessions. You can close the browser, come back later, and pick up where you left off. Only the last 20 messages are sent to the AI for context, keeping responses fast while preserving your full visible history.

---

## Why It Matters

- **Always available** — accessible from any page via the floating button. No need to navigate to a specific section to check on a site or look up a metric.
- **Real data, not guesses** — Alma queries your actual database and connected Google services. Every answer is grounded in your live data.
- **Reduces context-switching** — instead of jumping between Analytics, Search Console, and the AlmaSEO dashboard, ask Alma and get a combined answer in one place.
- **Helps diagnose problems fast** — failed automation jobs, traffic drops, and content gaps can be investigated conversationally without digging through logs.
- **Persistent memory** — your conversation carries across sessions, so you can reference earlier questions and build on previous answers.
- **Secure by design** — Alma only accesses sites you own, and sensitive data (passwords, API keys, OAuth tokens) is never included in responses.

---

## How to Use It

### Opening the Chat

1. Look for the **purple button** in the bottom-right corner of any page.
2. Click it to open the chat panel.
3. On first open, you'll see a welcome screen with Alma's introduction and four suggested prompts to get started.

### Asking Questions

1. Type your question in the input field at the bottom of the chat panel.
2. Press **Enter** to send.
3. Alma will display a typing indicator while she processes your question and queries any necessary data.
4. Her response appears in the chat — formatted with bold text, lists, and code blocks where appropriate.

### Suggested Starter Prompts

The welcome screen offers four quick prompts for new users:

- "What sites do I have?"
- "How is my automation performing?"
- "Show me my recent posts"
- "Are there any issues with my sites?"

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **Enter** | Send message |
| **Shift + Enter** | New line (without sending) |
| **Escape** | Close chat panel |

### Clearing the Conversation

Click the **trash icon** in the chat header to clear your entire conversation history and start fresh. This also resets the message counter.

---

## Key Settings / Options

### Limits

| Setting | Value | Notes |
|---------|-------|-------|
| Messages per session | 60 | Clear conversation to reset the counter |
| Max message length | 2,000 characters | Per individual message |
| Response timeout | 60 seconds | Client-side; try a simpler question if this triggers |
| Context window | Last 20 messages | Sent to the AI per request; full history stays visible in the UI |
| Max tool rounds | 3 per message | Prevents infinite loops when multiple tools are needed |
| Max response length | 1,000 tokens | Per AI response (~750 words) |

### AI Configuration

| Setting | Value |
|---------|-------|
| Model | GPT-4o-mini |
| Temperature | 0.7 |
| Response style | Under 300 words unless detail is needed |
| Scope | SEO, digital marketing, content strategy, and AlmaSEO features only |

### Data Access Requirements

| Data Source | Requirement |
|-------------|-------------|
| Site data, posts, jobs | Automatic — available for any site you own |
| Google Analytics | GA4 property connected via OAuth in Client Profile → Google Services |
| Google Search Console | GSC property connected via OAuth in Client Profile → Google Services |

### Privacy & Security

- Alma only returns data for sites owned by the requesting user.
- Passwords, API keys, OAuth tokens, and other credentials are stripped from all tool responses before being sent to the AI.
- Alma will not answer questions outside of SEO and digital marketing — she politely redirects off-topic queries.

---

## Notes / Edge Cases

- **Activity logging** — Alma automatically logs chat sessions to the Activity & Logs tab in Client Profile. Each site discussed gets one log entry per session showing the number of exchanges.
- **Token tracking** — total tokens used per session are tracked in the database for cost monitoring, but no hard token limit is enforced.
- **Credential fallback** — if a user-specific OAuth token is missing for GA or GSC, Alma falls back to any site-level token, improving reliability.
- **No tier gating** — Alma AI Chat is currently available to all authenticated users regardless of plan tier.
- **Single global session** — each user has one conversation thread (not per-site). Context changes as you navigate, but history is shared across all sites.
