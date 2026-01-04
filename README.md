# JoAi Knowledge Base

This repository contains all knowledge base articles for [JoAi](https://joai.ai).

## Structure

- `articles/{locale}/{category}/{slug}.md` - Article markdown files
- `images/{category}/{slug}/` - Article images and assets
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

1. Create article in `articles/{locale}/{category}/`
2. Add images to `images/{category}/{slug}/`
3. Commit and push to GitHub
4. App automatically fetches content on build

## Links

- Production: https://joai.ai/en/kb
- Repository: https://github.com/vLeapGroup/knowledge-base
