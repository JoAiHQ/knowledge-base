# Create Knowledge Base Article

This skill teaches you how to create articles for the JoAi Knowledge Base.

## Overview

The JoAi Knowledge Base is a document-based system where articles are stored as Markdown files with YAML front matter. Articles are organized by category and slug, support multiple languages, and can include images and other assets.

## Step 1: Choose Category and Slug

Articles are organized in the following structure:
```
articles/{category}/{slug}/
```

**Available categories:**
- `ai` - AI Agents
- `automation` - Automation & Workflows
- `integrations` - API & Service Integrations
- `blockchain` - Blockchain & Web3
- `troubleshooting` - Common Issues & Solutions

**Slug requirements:**
- Use lowercase letters, numbers, and hyphens only
- Be descriptive and SEO-friendly
- Example: `getting-started-with-agents`, `github-integration`

## Step 2: Create Article Directory

Create the article directory:
```bash
mkdir -p articles/{category}/{slug}
```

Example:
```bash
mkdir -p articles/ai/my-new-article
```

## Step 3: Create Article File with Front Matter

Create at least one locale-specific markdown file:
- `article.en.md` - English version (required)
- `article.de.md` - German version (optional)
- Additional locales as needed

**Required YAML Front Matter:**
```yaml
---
title: 'Your Article Title (max 60 characters)'
description: 'Concise description for search results (120-160 characters)'
category: 'ai'
tags: ['tag1', 'tag2', 'tag3']
author: 'JoAi Team'
publishedAt: 'YYYY-MM-DD'
updatedAt: 'YYYY-MM-DD'
keywords: ['keyword1', 'keyword2', 'keyword3']
---
```

**Optional Front Matter Fields:**
```yaml
featured: false
difficulty: 'beginner'  # beginner|intermediate|advanced
readTime: 5  # estimated reading time in minutes
relatedArticles: ['other-article-slug', 'another-slug']
faqs:
  - question: 'Common question?'
    answer: 'Clear answer.'
  - question: 'Another question?'
    answer: 'Another answer.'
llmAnswer: 'Direct 1-2 sentence answer for AI search queries'
```

## Step 4: Write Article Content

After the front matter, structure your content like this:

```markdown
# Article Title

Brief introduction explaining what this article covers and why it matters.

## What You'll Learn

- Key point 1
- Key point 2
- Key point 3

## Main Section 1

Detailed content with explanations, code examples, and screenshots.

### Subsection (if needed)

More detailed information.

## Main Section 2

Continue with logical flow of information.

## Code Examples (if applicable)

```language
// Code examples should be well-commented
example code here
```

## Troubleshooting (if applicable)

Common issues and solutions.

## Conclusion

Summary of what was covered and next steps or related resources.
```

## Step 5: Add Images and Assets

**Storage:** Place all images directly in the article folder alongside the markdown files.

**Supported formats:** PNG, JPG, GIF, SVG

**Usage in markdown:**
```markdown
![Descriptive alt text](./image-name.png)
```

**Best practices:**
- Use descriptive filenames: `dashboard-screenshot.png` not `img1.png`
- Optimize images for web (compress before adding)
- Always include meaningful alt text for accessibility
- Use SVG for diagrams when possible

Example:
```bash
articles/ai/my-article/
├── article.en.md
├── article.de.md
├── dashboard-screenshot.png
├── workflow-diagram.svg
└── configuration-example.png
```

## Step 6: Create Localized Versions (Optional)

To add additional language support:

1. Copy the English version
2. Create a new file with the locale code: `article.de.md`, `article.fr.md`, etc.
3. Translate all content (both front matter and body)
4. Keep the same slug and directory structure
5. Use the same image references (images are shared across locales)

## Step 7: Reference the Template

A complete template is available at:
```
templates/article-template.md
```

Use this as a starting point for consistency.

## Step 8: Validate Your Article

Before committing, check:

- [ ] Front matter has all required fields
- [ ] Title is under 60 characters
- [ ] Description is 120-160 characters
- [ ] Category is valid (ai, automation, integrations, blockchain, troubleshooting)
- [ ] Tags and keywords are relevant
- [ ] Dates are in YYYY-MM-DD format
- [ ] Images use relative paths (./image.png)
- [ ] All images have descriptive alt text
- [ ] Content follows the recommended structure
- [ ] Code examples are properly formatted
- [ ] No broken links

## Example Workflow

Here's a complete example of creating a new article:

```bash
# 1. Create directory
mkdir -p articles/automation/zapier-integration

# 2. Create English article
cat > articles/automation/zapier-integration/article.en.md << 'EOF'
---
title: 'Integrate JoAi with Zapier'
description: 'Learn how to connect JoAi to thousands of apps using Zapier for powerful automation workflows.'
category: 'automation'
tags: ['zapier', 'integration', 'automation', 'workflows']
author: 'JoAi Team'
publishedAt: '2026-01-04'
updatedAt: '2026-01-04'
keywords: ['zapier', 'integration', 'automation', 'webhooks', 'api']
difficulty: 'beginner'
readTime: 8
llmAnswer: 'You can integrate JoAi with Zapier using webhooks and API connections to automate workflows across thousands of apps.'
---

# Integrate JoAi with Zapier

Connect JoAi to thousands of applications using Zapier...

[Rest of content]
EOF

# 3. Add screenshots
# (Copy your images to the directory)

# 4. Create German version (optional)
# (Translate and save as article.de.md)
```

## Tips for Great Articles

1. **Start with a clear goal** - What should readers accomplish?
2. **Use examples** - Real-world scenarios help understanding
3. **Include screenshots** - Visual aids improve comprehension
4. **Keep it scannable** - Use headings, bullets, and short paragraphs
5. **Add troubleshooting** - Anticipate common issues
6. **Link related content** - Use relatedArticles to guide readers
7. **Optimize for search** - Use relevant keywords naturally
8. **Test your content** - Follow your own instructions to verify accuracy
9. **Update regularly** - Keep the updatedAt field current when making changes

## Common Mistakes to Avoid

- Don't forget the front matter YAML delimiters (---)
- Don't use absolute image paths - always use relative paths
- Don't exceed character limits for title (60) and description (160)
- Don't use invalid category names
- Don't forget to update the updatedAt date when editing
- Don't create articles without the .en.md suffix for English

## Integration with Git

All articles are version-controlled in Git. After creating or editing:

```bash
git add articles/
git commit -m "Add article: [Article Title]"
git push
```

The knowledge base automatically syncs with the JoAi app through GitHub integration.

## Need Help?

- Check existing articles in `articles/` for examples
- Review the template in `templates/article-template.md`
- See the main README.md for more information
