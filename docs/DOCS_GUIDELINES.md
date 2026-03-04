# AlmaSEO Documentation Guidelines

> **Audience:** Human contributors and Claude Code agents.
> If you are Claude Code, treat every rule in this file as a hard requirement.

---

## 1. Purpose

This file defines how AlmaSEO documentation is written, organized, and deployed.

**What "good docs" means for AlmaSEO right now:**

- **Coverage** — every shipped feature has a corresponding doc page.
- **Consistency** — every feature doc follows the same template and naming conventions.
- **Reliable deploys** — every push to `main` triggers a Netlify build that goes live without manual intervention.

---

## 2. Source of Truth + Repo Rules

| Rule | Detail |
|------|--------|
| **Repo** | `ilaos/myproject-docs` is the only repo for public documentation. |
| **Editable files** | Only edit Markdown files inside `/docs`. |
| **Generated output** | **NEVER** edit or commit anything in `/site`. Netlify builds this automatically. |
| **Branch** | Commit directly to `main` for all docs changes (this triggers Netlify). |
| **Workflow** | `git add` the changed files, `git commit`, `git push origin main`. |

**Claude Code — hard rules:**

- Do not create feature branches for docs-only changes.
- Do not touch `/site` under any circumstances.
- After every change, push to `main` so Netlify picks it up.

---

## 3. Netlify Deployment

| Item | Value |
|------|-------|
| **Live site** | [https://docs.almaseo.com](https://docs.almaseo.com) |
| **Trigger** | Push to `main` branch |
| **Build command** | `pip install -r requirements.txt && mkdocs build` |
| **Publish directory** | `site` |

**Expected behavior:**

1. You push to `main`.
2. Netlify detects the push and runs the build command.
3. The built `/site` directory is deployed.
4. Changes are live at `https://docs.almaseo.com` within ~1-2 minutes.

If the build fails, check that:

- All nav entries in `mkdocs.yml` point to files that actually exist.
- No broken Markdown syntax or unclosed frontmatter blocks.

---

## 4. Where New Feature Docs Go

AlmaSEO docs use a **Feature Catalog** structure.

- **Location:** All feature docs live under `docs/features/`.
- **Index:** Every new feature doc must be linked from `docs/features/index.md`.
- **mkdocs.yml:** Do **NOT** modify `mkdocs.yml` unless explicitly instructed by the user.

### File naming rules

- Use **kebab-case**: lowercase words separated by hyphens.
- Keep names short and descriptive.
- Examples: `internal-linking.md`, `email-reports.md`, `schema-generator.md`.

### Subdirectories

If a feature area has multiple pages, group them in a subdirectory:

```
docs/features/content-creation/
docs/features/content-creation/index.md
docs/features/content-creation/article-types.md
```

---

## 5. Feature Doc v1 Template

Copy this template when creating a new feature doc. Remove sections that don't apply, but keep the order.

````markdown
---
title: "Feature Name"
slug: "feature-slug"
type: "feature"
status: "draft"
tier: "Pro"
feature_id: ""
last_updated: "YYYY-MM-DD"
---

# Feature Name

## Overview

One or two sentences explaining what this feature is.

## What It Does

Describe the feature's behavior. What happens when the user interacts with it?

## Why It Matters

- Benefit 1
- Benefit 2
- Benefit 3

## How to Use It

1. Step one
2. Step two
3. Step three

## Key Settings / Options

| Setting | Default | Description |
|---------|---------|-------------|
| Example | `true`  | What it controls |

## Notes / Edge Cases

- Any known limitations or special behavior.
````

---

## 6. Frontmatter Schema

Every feature doc should include YAML frontmatter at the top of the file. This is lightweight now but enables future automation (index generation, status dashboards, etc.).

```yaml
---
title: "Feature Name"          # Human-readable feature name
slug: "feature-slug"           # Matches the filename (without .md)
type: "feature"                # Always "feature" for feature docs
status: "draft"                # draft | complete
tier: "Pro"                    # Core/Free | Pro | Agency | Pro/Agency
feature_id: "XX-FEAT-NAME"    # Internal feature ID (e.g., PL-AI-CHAT, CC-BLOG-ART)
last_updated: "YYYY-MM-DD"    # Date of last meaningful edit
---
```

**Rules:**

- `slug` must match the filename. If the file is `email-reports.md`, the slug is `email-reports`.
- `status` starts as `draft`. Set to `complete` only when the doc is reviewed and accurate.
- `tier` indicates the minimum pricing tier required to access the feature. Use one of: `Core/Free`, `Pro`, `Agency`, or `Pro/Agency`.
- `feature_id` is the internal identifier used in the codebase and roadmap (e.g., `PL-AI-CHAT`). If unknown, leave as an empty string `""`.
- `last_updated` must be set to the current date whenever the doc content changes.

---

## 7. Change Process

Follow these steps for every documentation change.

### Adding a new feature doc

1. **Create the file** in `docs/features/` using the template from Section 5.
2. **Update `docs/features/index.md`** — add a link to the new doc.
3. **Sanity check** — confirm the link path matches the actual file path.
4. **Commit and push:**
   ```bash
   cd /root/myproject-docs
   git add docs/
   git commit -m "docs: add <feature-name> documentation"
   git push origin main
   ```
5. **Confirm deploy** — verify Netlify shows a new deploy triggered by your push.

### Editing an existing doc

1. Edit the file.
2. Update `last_updated` in frontmatter.
3. Commit and push.

### Claude Code checklist (run mentally before every push)

- [ ] Only files under `/docs` were modified.
- [ ] No changes to `/site`.
- [ ] New docs are linked from `features/index.md`.
- [ ] Frontmatter is present and valid.
- [ ] File uses kebab-case naming.
- [ ] Commit message starts with `docs:`.
