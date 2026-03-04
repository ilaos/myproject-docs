---
title: "Content Creation"
slug: "content-creation"
type: "feature"
status: "complete"
tier: "Core/Free"
feature_id: "CC"
last_updated: "2026-03-04"
---

# Content Creation

## Overview

Content Creation is the core engine of AlmaSEO. It takes a topic and a set of preferences — article type, tone, length, language, keywords — and produces a complete, publication-ready article with SEO metadata, a featured image, and one-click publishing to WordPress or export to any platform.

Every article is powered by OpenAI GPT-4 models with AlmaSEO's proprietary **Content Authority Engine** running behind the scenes. The Content Authority Engine eliminates AI-sounding language, injects real E-E-A-T signals from the business profile, enforces structural depth based on content length, and produces decisive, action-oriented writing — not generic filler.

The system supports **11 article types**, **28 languages**, **4 writing tones**, **3 content lengths**, and multiple publishing and export formats. Content generation runs in the background, so users can continue working while articles are being created.

---

## What It Does

### The End-to-End Flow

1. **User opens the Article Creation Form** (`/create-post`)
2. **Selects a site** and chooses an article type
3. **Configures the article** — topic, tone, length, language, keywords, special instructions, featured image preferences, and publishing options
4. **Submits the form** — AlmaSEO creates a record and launches background generation
5. **AI generates the content** — the Content Authority Engine assembles the article with E-E-A-T signals, humanized writing, and structural depth
6. **Featured image is generated** (if selected) — via DALL-E 3 or Gemini
7. **Article lands on the Post Details page** — ready for review, editing, publishing, or export
8. **Publishing** — auto-publish to WordPress, save as draft, or export to any platform

### 11 Article Types

Each type has its own generation logic, prompt structure, and output format tailored to its purpose.

| Type | Best For | Special Features |
|------|----------|-----------------|
| **Blog Article** | Regular blog content, news, thought leadership | SEO optimization, internal linking, CTAs |
| **Service Page** | Describing a business service | Uses services offered, pricing, location emphasis |
| **City/County/State Page** | Local SEO landing pages | Address integration, service area targeting |
| **FAQ Page** | Common questions about a topic | Q&A structure, FAQ schema generation |
| **Freestyle** | Anything — user provides full instructions | User-supplied instructions override all templates |
| **Glossary / Terms** | Industry terminology and definitions | Definition format, industry-specific terms |
| **How-To Guide** | Step-by-step instructional content | Numbered steps, HowTo schema support |
| **About Us Page** | Company/team introduction | Draws from business profile, tenure, team data |
| **Pillar Content** | Comprehensive, long-form cornerstone pages | Longest format (1400-1800+ words), 6-8 sections |
| **Listicle** | Top 10 lists, roundups, ranked items | Numbered list format, engagement-focused |
| **Comparison (X vs Y)** | Side-by-side product or service comparisons | Two-sided analysis with clear verdict |

### Content Authority Engine

Every article passes through AlmaSEO's proprietary Content Authority Engine — a set of six systems that run behind every generation to ensure the output reads like it was written by an industry expert, not an AI.

| Component | What It Does |
|-----------|-------------|
| **Humanization Protocol** | Eliminates AI fingerprints — bans robotic openings ("Have you ever..."), overused adjectives ("incredibly", "amazing"), and formulaic transitions. Uses varied sentence structures and natural flow. |
| **E-E-A-T Integration** | Injects real Experience, Expertise, Authoritativeness, and Trust signals pulled from the business profile — tenure years, owner name, services offered, industry type. Maps 100+ industries to authority titles (Attorney, Technician, Specialist, etc.). |
| **Structural Depth Quotas** | Enforces document structure based on content length. Short: 3-5 sections. Medium: 4-6 sections with H3 sub-sections. Long: 6-8 sections with 2+ H3s each. LSI keywords woven throughout. |
| **Decision Intelligence** | Produces clear, opinionated content. Bans hedging language ("may", "could", "might"). Strong conclusions and definitive guidance. |
| **Conversion Architecture** | Action-oriented headings, CTAs aligned to business goals, HowTo/FAQ schema where applicable, and internal linking to related content (up to 3 links per article). |
| **LSI Keyword Integration** | Semantic keyword variations and long-tail phrases woven naturally into the content — not stuffed. |

### Content Output

Every generated article includes:

| Component | Description |
|-----------|-------------|
| **HTML content** | Full article formatted as HTML, ready for WordPress or web publishing |
| **Structured content** | JSON representation for multi-format export (Markdown, MDX, JSON, etc.) |
| **SEO metadata** | Title tag, meta description, and focus keywords |
| **Featured image** | AI-generated (DALL-E 3 or Gemini) or uploaded/Unsplash image |
| **Word count** | Tracked against target for the selected content length |
| **Readability scores** | Flesch Reading Ease, passive voice %, sentence length, paragraph length, transition words |
| **Progress log** | Real-time status updates visible during generation |

### Content Inventory

Before writing, users can review what content already exists on their site to avoid duplication:

- **WordPress Content Pull** — fetches existing posts and pages via the WordPress REST API
- **Sitemap & Scrape Discovery** — parses sitemaps (including gzipped) to discover all indexed pages, with web scraping fallback
- **Search & Filter** — client-side search across all discovered content
- **Similar Article Detection** — when creating a new article, the system checks for similar existing content and warns the user with confidence scores

### Publishing & Export

| Option | Description |
|--------|-------------|
| **Auto-Publish to WordPress** | Publishes directly as a live post with SEO metadata written to the active SEO plugin |
| **Draft to WordPress** | Pushes as a WordPress draft for review before publishing |
| **Multi-Format Export** | Download as HTML, HTML body only, Markdown, JSON, MDX, or YAML |
| **Quick Copy** | Copy raw content, HTML, or Markdown to clipboard |
| **Featured Image Export** | Download the generated image as PNG/JPEG |
| **Static Site Export** | Export panel for non-WordPress sites with all format options |
| **IndexNow Submission** | Submit the published URL to Bing for fast indexing |
| **Search Console Submission** | Submit the URL to Google Search Console for indexing |
| **Publication Report Email** | Email notification with article summary after publishing |

### Post Details Page

After generation, the Post Details page (`/post/<id>`) is the hub for reviewing, validating, and acting on the content:

- **Quick Info** — title, topic, status, word count, dates
- **Content Preview** — live preview of the full article
- **SEO Metadata** — title, description, and keywords (editable)
- **Readability Scores** — Flesch score, passive voice, sentence/paragraph metrics
- **Google NLP Validation** — entity analysis, sentiment, syntax scoring via Google Natural Language API
- **SEO Insights** — AI-powered recommendations for improving the title, description, and keywords
- **Content Analysis** — generation time, language, creation timestamp
- **Search Console Indexing** — indexing status and submission
- **Export Options** — all formats available for download or copy
- **Action Buttons** — publish, regenerate, edit, delete, mark as published, submit to IndexNow/GSC

---

## Why It Matters

- **Full articles in under 2 minutes** — from topic to publication-ready content with metadata and a featured image, without leaving the platform.
- **Not generic AI content** — the Content Authority Engine produces articles grounded in real business data (E-E-A-T), with human-sounding language and decisive expertise. This is content that ranks, not content that reads like ChatGPT.
- **11 purpose-built article types** — each type has its own generation logic. A Service Page reads differently from a Blog Article, which reads differently from a FAQ. The AI knows the difference.
- **28 languages, natively** — content is generated in the target language, not translated. The AI writes directly in Spanish, French, German, Arabic, Japanese, and 23 other languages.
- **Publish anywhere** — WordPress auto-publish, static site export, Markdown for Hugo/Jekyll, MDX for Next.js, JSON for headless CMS. One article, every format.
- **Duplicate prevention** — Content Inventory and Similar Article Detection stop you from writing what already exists.
- **SEO metadata handled automatically** — title tags, meta descriptions, Open Graph, and schema are generated and written to the correct SEO plugin fields (AIOSEO, Yoast, Rank Math) without manual entry.
- **Quality verification built in** — readability scores, Google NLP validation, and AI-powered SEO insights give you confidence before publishing.

---

## How to Use It

### Creating an Article

1. Navigate to **Create Post** (`/create-post`) from the sidebar.
2. **Select the target site** from the dropdown.
3. **Choose an article type** — the form updates to show fields relevant to that type.
4. **Enter the topic** — or service name, city, FAQ area, etc., depending on the type.
5. **Configure optional settings:**
   - **Writing Tone** — Professional, Friendly, Authoritative, or Conversational
   - **Content Length** — Short (500-700 words), Medium (800-1000), or Long (1200-1500)
   - **Content Language** — choose from 28 supported languages
   - **Target Keywords** — comma-separated keywords to weave into the content
   - **Special Instructions** — free-text instructions that take highest priority in generation
   - **Featured Image** — Generate (AI), Upload, Unsplash, or None
   - **WordPress Categories** — select or create categories (WordPress sites only)
   - **Custom Permalink** — set a custom URL slug (WordPress sites only)
6. **Choose publishing mode:**
   - **Publish Immediately** — auto-publishes to WordPress as a live post
   - **Draft** (default) — saves as draft for review
   - **Content Brief Only** — outputs a brief instead of a full article (for human writers)
7. Click **Generate** — the article is created in the background.
8. You'll be redirected to the **Post Details page** where you can watch progress and review the result.

### Reviewing & Publishing

1. On the **Post Details page**, review the generated content, SEO metadata, and readability scores.
2. Use **Google NLP Validation** and **SEO Insights** to check quality.
3. Edit the content or metadata if needed.
4. **Publish** to WordPress, **export** in your preferred format, or **copy** to clipboard.
5. Optionally submit to **IndexNow** or **Google Search Console** for fast indexing.

---

## Key Settings / Options

### Writing Tone

| Tone | Style | Direct Address (you/your) |
|------|-------|--------------------------|
| Professional | Formal, third-person, B2B-focused | No |
| Friendly | Warm, approachable, relatable | Yes |
| Authoritative | Expert, confident, knowledge-driven | No |
| Conversational | Casual, natural, easygoing | Yes |

### Content Length

| Length | Word Target | Structure |
|--------|------------|-----------|
| Short | 500-700 words | 3-5 sections |
| Medium | 800-1000 words | 4-6 sections with H3 sub-sections |
| Long | 1200-1500 words | 6-8 sections with 2+ H3s each |

### Featured Image Options

| Option | Source | Configuration |
|--------|--------|--------------|
| Generate (AI) | DALL-E 3 (default) or Gemini | Aspect ratio (1:1, 16:9, 3:2, 2:3, 3:4, 4:3, 9:16), custom description |
| Upload | User file | Any image format |
| Unsplash | Unsplash API | Search by keyword |
| None | — | No featured image |

### Supported Languages (28)

English, Spanish, French, German, Italian, Portuguese, Dutch, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Polish, Turkish, Swedish, Norwegian, Danish, Finnish, Greek, Hebrew, Czech, Romanian, Hungarian, Thai, Vietnamese, Indonesian, Malay

### AI Models

| Use Case | Model |
|----------|-------|
| Blog, Service, City Landing, FAQ | GPT-4-turbo |
| Glossary, How-To, About Us, Pillar, Listicle, Comparison | GPT-4o |
| Freestyle | GPT-4 |
| Featured Images (default) | DALL-E 3 |
| Featured Images (alternative) | Gemini 2.5 Flash |

### SEO Plugin Compatibility

Generated SEO metadata is automatically written to the correct fields for:

- All in One SEO (AIOSEO) — Free and Pro
- Yoast SEO
- Rank Math
- SEOPress
- The SEO Framework

---

## Notes / Edge Cases

- **Background generation** — all content is generated in a background thread. The form submission returns immediately and redirects to the Post Details page, where a progress indicator shows real-time status updates.
- **Generation time** — typical articles complete in 45-76 seconds. During OpenAI peak hours, this can spike to 120+ seconds.
- **Similar article warnings** — the creation form checks for existing content with similar topics and shows a warning with confidence scores. This can be overridden.
- **GBP testimonials** — if the site has Google Business Profile connected, 5-star customer reviews are automatically pulled and woven into blog articles as social proof.
- **Internal linking** — the generator automatically adds up to 3 internal links to related existing content on the site.
- **Content Brief mode** — when toggled on, the system outputs a detailed content brief (outline, key points, keyword targets) instead of a full article, intended for human writers.
- **Centralized Prompt System** — all generation uses a centralized prompt manager (`utils/prompt_manager.py`) with layered prompts and business context injection. Legacy prompts exist as fallback only.

### Sub-features

- **[Generate Content Brief Only](generate-content-brief-only.md)** *(Agency)* — Outputs a detailed content brief instead of a full article.
- **[Article Types](article-types.md)** *(Core/Free)* — 11 content types, each with specialized logic.
- **[Content Inventory](content-inventory.md)** *(Pro)* — See everything that exists before you write.
- **[Content Output](content-output.md)** *(Core/Free)* — What gets generated with every article.
- **[Publishing & Export](publishing-export.md)** *(Core/Free)* — Deliver content to any platform.
- **[Article Creation Form](article-creation-form.md)** *(Core/Free)* — The central interface for configuring a new article.
- **[Post Details](post-details.md)** *(Core/Free)* — The post-creation hub for viewing, validating, and acting on generated content.
- **[GBP Testimonials in Generated Articles](gbp-testimonials-in-generated-articles.md)** *(Pro)* — Automatically pulls real 5-star reviews into blog articles.
