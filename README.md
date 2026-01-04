# JoAi Knowledge Base

This repository contains all knowledge base articles for [JoAi](https://joai.ai).

## Structure

- `articles/{category}/{slug}/article.{locale}.md` - Locale-specific article files (e.g., `article.en.md`, `article.de.md`)
- `articles/{category}/{slug}/article.md` - Universal article file (fallback when no locale-specific version exists)
- `articles/{category}/{slug}/*.png|jpg|gif|svg` - Embedded images and assets (referenced with relative paths like `./image.png`)
- `templates/` - Templates for creating new articles

## Locales

- `en` - English (default)
- `de` - German

## Categories

- `ai` - AI Agents
- `automation` - Automation & Workflows
- `integrations` - API & Service Integrations
- `blockchain` - Blockchain & Web3
- `troubleshooting` - Common Issues & Solutions

## Creating Articles

See the article template in `templates/article-template.md`

### Front Matter Format

Every article must include front matter with these required fields:

```yaml
---
title: 'Article Title (max 60 chars)'
description: 'Description 120-160 chars'
category: 'ai|automation|integrations|blockchain|troubleshooting'
tags: ['tag1', 'tag2']
author: 'JoAi Team'
publishedAt: 'YYYY-MM-DD'
updatedAt: 'YYYY-MM-DD'
keywords: ['keyword1', 'keyword2', 'keyword3']
---
```

## Workflow

1. Create article folder: `articles/{category}/{slug}/`
2. Add article file(s):
   - `article.en.md` for English version
   - `article.de.md` for German version
   - `article.md` for universal/fallback version
3. Add images directly to the article folder and reference with relative paths: `![Alt text](./image.png)`
4. Commit and push to GitHub
5. App automatically fetches content on build

### Image References

Images should be placed directly in the article folder and referenced with relative paths:

```markdown
![Dashboard](./dashboard.png)
![Workflow Diagram](./workflow-diagram.svg)
```

## Links

- Production: https://joai.ai/en/kb
- Repository: https://github.com/vLeapGroup/knowledge-base
