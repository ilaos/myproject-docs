# Role-Based Feature Access

This matrix shows which features are accessible to each user role. Use this guide when setting up team permissions for agency accounts.

## Role Hierarchy

AlmaSEO uses a hierarchical role system where each role includes all permissions of the roles below it:

| Role | Description |
|------|-------------|
| **Owner / Admin** | Full platform access including automation controls, guardrails, and system settings |
| **Manager** | Site management, WordPress settings, publishing controls, and export tools |
| **SEO Manager** | Client profiles, SEO tools, content intelligence, analytics, and integrations |
| **Client (read-only)** | View-only access to analytics and reporting dashboards |
| **Writer** | Content creation, article types, editing, and basic publishing |

!!! info "Permission Modes"
    Most features support **Configurable per client** permissions, meaning access can be customized on a per-site basis. Some features use **Configurable per user** (set per team member) or **Fixed** (cannot be changed).

---

## Feature Access Matrix

### Content Creation

| Feature | Tier | Writer | SEO Manager | Manager | Owner/Admin | Permission Mode |
|---------|------|--------|-------------|---------|-------------|------------------|
| Content Creation | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Article Types | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Content Inventory | Pro | ✅ | ✅ | ✅ | ✅ | Per client |
| Content Output | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Publishing & Export | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Sitemap & Scrape Discovery | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Search & Filter | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Blog Article | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Service Page | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| City/County/State Page | Agency | ✅ | ✅ | ✅ | ✅ | Per client |
| FAQ Page | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Freestyle | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Glossary Terms | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| How-To Guide | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| About Us Page | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Pillar Content | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Listicle | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Comparison (X vs Y) | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Featured Image Generation | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| SEO Metadata Package | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Multi-Format Export | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Quick Copy Options | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Featured Image Export | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Article Creation Form | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Writing Tone | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Content Length | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Content Language | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Generate Content Brief Only | Agency | ✅ | ✅ | ✅ | ✅ | Per client |
| Custom Permalink | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Target Keywords | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Wordpress Categories | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Special Instructions | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Parent Page & Page Order | Pro | ✅ | ✅ | ✅ | ✅ | Per client |
| Featured Image | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Post Details | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Quick Info | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| SEO Metadata | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| SEO Insights | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Content Analysis | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Include Image at Top of Article | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| Static Site Export Panel | Core/Free | ✅ | ✅ | ✅ | ✅ | Per client |
| GBP Testimonials in Generated Articles | Pro | ✅ | ✅ | ✅ | ✅ | Per client |
| WordPress Content Pull | Core/Free | — | — | ✅ | ✅ | Per client |
| Auto-Publish to WordPress | Core/Free | — | — | ✅ | ✅ | Per user |
| Publication Report Email | Pro | — | — | ✅ | ✅ | Per user |
| Publish Immediately | Core/Free | — | — | ✅ | ✅ | Per user |
| Publication Report Email | Pro | — | — | ✅ | ✅ | Per user |
| Search Console Indexing | Pro | — | — | ✅ | ✅ | Per user |
| IndexNow Submission | Pro | — | — | ✅ | ✅ | Per user |
| Google NLP Validation | Pro | — | — | ✅ | ✅ | Per user |
| Mailchimp Article Blast | Pro | — | — | ✅ | ✅ | Per user |
| Social Media Sharing | Pro | — | — | ✅ | ✅ | Per user |
| Content Pipeline | Pro | — | — | ✅ | ✅ | Per client |
| Topic Scheduling | Pro | — | — | ✅ | ✅ | Per client |
| Monitoring | Pro | — | — | ✅ | ✅ | Per client |
| Automation Settings | Pro | — | — | ✅ | ✅ | Per client |

### Client Management

| Feature | Tier | Writer | SEO Manager | Manager | Owner/Admin | Permission Mode |
|---------|------|--------|-------------|---------|-------------|------------------|
| Analytics & Insights | Agency | — | ✅ | ✅ | ✅ | Per client |
| Analytics | Pro | — | ✅ | ✅ | ✅ | Per client |
| Client Profile | Agency | — | ✅ | ✅ | ✅ | Per client |
| SEO Operations | Agency | — | ✅ | ✅ | ✅ | Per client |
| Backlinks & Outreach | Agency | — | ✅ | ✅ | ✅ | Per client |
| Overview | Pro | — | ✅ | ✅ | ✅ | Per client |
| Social Profiles | Pro | — | ✅ | ✅ | ✅ | Per client |
| Content Hub | Pro | — | ✅ | ✅ | ✅ | Per client |
| Published Posts | Pro | — | ✅ | ✅ | ✅ | Per client |
| Drafts | Pro | — | ✅ | ✅ | ✅ | Per client |
| Scheduled Posts | Pro | — | ✅ | ✅ | ✅ | Per client |
| First Impression Tool | Pro | — | ✅ | ✅ | ✅ | Per client |
| Website Analysis | Pro | — | ✅ | ✅ | ✅ | Per client |
| SEO Recovery 911 | Pro | — | ✅ | ✅ | ✅ | Per client |
| GEO/AI Search Optimizer | Pro | — | ✅ | ✅ | ✅ | Per client |
| Opportunities | Pro | — | ✅ | ✅ | ✅ | Per client |
| Backlinks Overview | Pro | — | ✅ | ✅ | ✅ | Per client |
| Live Links | Pro | — | ✅ | ✅ | ✅ | Per client |
| Backlinks | Pro | — | ✅ | ✅ | ✅ | Per client |
| Activity & Logs | Pro/Agency | — | ✅ | ✅ | ✅ | Per client |
| Site Management | Agency | — | — | ✅ | ✅ | Per user |
| Business Information | Core/Free | — | — | ✅ | ✅ | Per client |
| Locations | Pro | — | — | ✅ | ✅ | Per client |
| NAP Shield | Agency | — | — | ✅ | ✅ | Per client |
| Services & Areas | Pro | — | — | ✅ | ✅ | Per client |
| Wordpress Settings | Core/Free | — | — | ✅ | ✅ | Per client |
| Content AI | Pro | — | — | ✅ | ✅ | Per client |
| Search Console | Pro | — | — | ✅ | ✅ | Per client |
| Google Ads | Agency | — | — | ✅ | ✅ | Per client |
| Business Profile | Pro | — | — | ✅ | ✅ | Per client |
| Google Services | Pro | — | — | ✅ | ✅ | Per client |
| GBP Business Info → NAP Shield Ground Truth | Agency | — | — | ✅ | ✅ | Per client |
| Ownership Tracker | Agency | — | — | ✅ | ✅ | Fixed |
| Infrastructure Scan | Pro | — | — | ✅ | ✅ | Per client |
| Hosting | Pro | — | — | ✅ | ✅ | Per client |
| Email Providers | Pro | — | — | ✅ | ✅ | Per client |
| Scan Overview | Pro | — | — | ✅ | ✅ | Per client |
| SSL & Security | Pro | — | — | ✅ | ✅ | Per client |
| Domain & DNS | Pro | — | — | ✅ | ✅ | Per client |
| Outreach | Agency | — | — | ✅ | ✅ | Per user |
| Content Automation | Pro | — | — | ✅ | ✅ | Per user |
| Client Work Report Email | Pro/Agency | — | — | ✅ | ✅ | Per user |

### Content Intelligence

| Feature | Tier | Writer | SEO Manager | Manager | Owner/Admin | Permission Mode |
|---------|------|--------|-------------|---------|-------------|------------------|
| Content Intelligence | Pro | — | ✅ | ✅ | ✅ | Per client |
| AI Content Recommendations | Pro | — | ✅ | ✅ | ✅ | Per client |
| Intelligence Data Sources | Core/Free | — | ✅ | ✅ | ✅ | Per client |
| Search Visibility Opportunities | Pro | — | ✅ | ✅ | ✅ | Per client |
| Content Hierarchy Warnings | Pro | — | ✅ | ✅ | ✅ | Per client |
| Semantic Duplicate Detection | Pro | — | ✅ | ✅ | ✅ | Per client |
| Content-Type-Specific Logic | Core/Free | — | ✅ | ✅ | ✅ | Per client |
| Live Market Context | Core/Free | — | ✅ | ✅ | ✅ | Per client |
| Underserved Category Detection | Pro | — | ✅ | ✅ | ✅ | Per client |
| Click-to-Fill Topic Selection | Core/Free | — | ✅ | ✅ | ✅ | Per client |
| Live Market Context | Pro | — | ✅ | ✅ | ✅ | Per client |
| Static Site Inventory | Core/Free | — | ✅ | ✅ | ✅ | Per client |
| GBP Search Queries → AI Recommendations | Pro | — | ✅ | ✅ | ✅ | Per client |
| Reviews → Content Mining for Blog Topics | Pro | — | ✅ | ✅ | ✅ | Per client |
| WordPress Content | Core/Free | — | — | ✅ | ✅ | Per client |
| WordPress Categories | Core/Free | — | — | ✅ | ✅ | Per client |
| Google Search Console | Pro | — | — | ✅ | ✅ | Per client |
| Business Profile | Core/Free | — | — | ✅ | ✅ | Per client |

### Content Authority

| Feature | Tier | Writer | SEO Manager | Manager | Owner/Admin | Permission Mode |
|---------|------|--------|-------------|---------|-------------|------------------|
| Content Authority Engine | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| Humanization Protocol | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| E-E-A-T Integration | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| Structural Depth Quotas, | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| Decision Intelligence | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| Conversion Architecture | Core/Free | ✅ | ✅ | ✅ | ✅ | Fixed |
| Structured Data (Schema) | Pro | — | ✅ | ✅ | ✅ | Per client |
| First Impression — Schema Generator (Manual Tool) | Pro | — | ✅ | ✅ | ✅ | Per client |
| Schema Detection & Scoring (Background Analysis) | Pro | — | ✅ | ✅ | ✅ | Per client |
| Static Export Schema (Automated Pipeline) | Pro | — | ✅ | ✅ | ✅ | Per client |
| Structured Data Dashboard & WordPress Injection | Agency | — | — | ✅ | ✅ | Per client |
| WordPress Gutenberg Schema Panel (Editor Integration) | Pro | — | — | ✅ | ✅ | Per client |

### Platform

| Feature | Tier | Writer | SEO Manager | Manager | Owner/Admin | Permission Mode |
|---------|------|--------|-------------|---------|-------------|------------------|
| Alma AI Chat — Global AI Assistant | Pro/Agency | ✅ | ✅ | ✅ | ✅ | Per user |
| AlmaSEO WordPress Connector Plugin | Pro | — | — | ✅ | ✅ | Fixed |
| Guardrails & Safety | Pro | — | — | — | ✅ | Fixed |
| Monitoring & Logs | Pro | — | — | — | ✅ | Fixed |
| Automation Center | Pro | — | — | — | ✅ | Fixed |

---

## Access Level Summary

- **Writer**: 49 features
- **SEO Manager**: 87 features
- **Manager**: 131 features
- **Owner / Admin**: 134 features

**Total features:** 134

---

## Customizing Permissions

Most features support per-client or per-user permission overrides:

- **Per client**: Access can be toggled on/off for each site in the Client Profile settings
- **Per user**: Access can be configured for individual team members in User Management
- **Fixed**: Access level cannot be changed — determined by the user's role

When a feature is marked "Configurable per client," the Default Access column shows who has access by default. An Owner/Admin can then expand or restrict access for specific sites.
