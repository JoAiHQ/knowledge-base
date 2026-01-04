# Create Knowledge Base Article

This skill teaches you how to create SEO-optimized articles for the JoAi Knowledge Base.

## Overview

The JoAi Knowledge Base is a document-based system where articles are stored as Markdown files with YAML front matter. Articles are organized by category and slug, support multiple languages, and can include images and other assets.

**PRIMARY GOAL: MAXIMIZE SEO & AI SEARCH DISCOVERY** - Every article must be optimized for:
1. **Traditional Search Engines** (Google, Bing) - Drive organic traffic through keyword optimization
2. **AI Search Systems** (ChatGPT, Claude, Perplexity) - Ensure AI assistants can discover and cite your content

SEO and AI discoverability considerations should guide ALL decisions from slug selection to content structure.

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

**Slug requirements (CRITICAL FOR SEO):**
- Use lowercase letters, numbers, and hyphens only
- Include target keyword in the slug
- Be descriptive, specific, and match search intent
- Keep it concise but meaningful (3-5 words ideal)
- Think: "What would someone search for to find this?"

**Good examples:**
- `getting-started-with-agents` (targets "getting started with agents")
- `github-integration-guide` (targets "github integration")
- `fix-authentication-errors` (targets specific problem)

**Bad examples:**
- `article-1` (no keywords, not descriptive)
- `new-feature` (too vague)
- `my-article` (not search-friendly)

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

**Required YAML Front Matter (SEO-CRITICAL):**
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

**SEO Optimization Guidelines for Front Matter:**

**Title (MOST IMPORTANT FOR SEO):**
- MUST include primary target keyword
- Keep under 60 characters (displays fully in search results)
- Front-load important keywords
- Make it compelling and clickable
- Examples:
  - Good: "GitHub Integration Guide for JoAi - Complete Setup"
  - Bad: "How to Use the Integration Feature"

**Description (CRITICAL FOR CLICK-THROUGH RATE):**
- MUST be 120-160 characters (optimal for search snippets)
- Include primary keyword naturally
- Include a clear value proposition or benefit
- Use action words when appropriate
- Examples:
  - Good: "Learn how to connect JoAi to GitHub in 5 minutes. Automate workflows, sync repos, and boost productivity with our step-by-step guide."
  - Bad: "This article explains the GitHub integration."

**Keywords (FOR SEARCH TARGETING):**
- List 5-10 relevant keywords/phrases
- Include primary keyword (from title)
- Add semantic variations and long-tail keywords
- Think about user search intent
- Include common misspellings if relevant
- Examples: ['github integration', 'connect github joai', 'github automation', 'sync github repository', 'github api setup']

**Tags (FOR INTERNAL ORGANIZATION & TOPIC CLUSTERING):**
- Use 3-5 specific, relevant tags
- Support SEO through content clustering
- Help users discover related content

**Optional Front Matter Fields (HIGHLY RECOMMENDED FOR SEO):**
```yaml
llmAnswer: 'Direct 1-2 sentence answer for AI search queries'
faqs:
  - question: 'Common question?'
    answer: 'Clear answer.'
  - question: 'Another question?'
    answer: 'Another answer.'
featured: false
difficulty: 'beginner'  # beginner|intermediate|advanced
readTime: 5  # estimated reading time in minutes
relatedArticles: ['other-article-slug', 'another-slug']
```

**llmAnswer (CRITICAL FOR AI SEARCH DISCOVERY):**
- This field is THE MOST IMPORTANT for AI search engines (ChatGPT, Claude, Perplexity, etc.)
- Provide a concise, direct answer to the main question your article addresses
- Use 1-2 sentences maximum
- Include key terms and specific details
- AI assistants will cite this when users ask related questions
- Examples:
  - Good: "You can integrate JoAi with GitHub using webhooks and the GitHub API. The setup takes 5 minutes and enables automatic workflow synchronization."
  - Bad: "This article explains GitHub integration." (too vague)
  - Good: "To fix authentication errors in JoAi, verify your API key is correct and check that your account has the required permissions in Settings > API Access."
  - Bad: "There are several ways to fix this." (not specific)

**FAQs (BOOSTS SEO & AI DISCOVERY):**
- Add 3-5 frequently asked questions related to your topic
- Each FAQ should target long-tail search queries
- Write questions as users would search them
- Provide clear, direct answers
- FAQs help with:
  - Featured snippets in Google
  - "People also ask" sections
  - AI search result citations
- Examples:
  - "How long does GitHub integration setup take?" → "Setup takes approximately 5 minutes."
  - "Do I need a paid GitHub account?" → "No, JoAi works with both free and paid GitHub accounts."

**relatedArticles (FOR INTERNAL LINKING & SEO):**
- Link 2-4 related articles by slug
- Helps with topic clustering and site authority
- Improves user engagement metrics (reduces bounce rate)
- Helps search engines understand content relationships

## Step 4: Write SEO-Optimized Article Content

After the front matter, structure your content for maximum SEO impact:

```markdown
# Article Title

[First paragraph MUST include primary keyword within first 100 words]
Brief introduction explaining what this article covers and why it matters.
Include the target keyword naturally 2-3 times in the intro.

## What You'll Learn

- Key point 1 (include keyword variations)
- Key point 2
- Key point 3

## Main Section 1 [Use keyword-rich headings]

Detailed content with explanations, code examples, and screenshots.
Use keywords naturally throughout (target 1-2% keyword density).

### Subsection [H3 headings for detailed topics]

More detailed information.

## Main Section 2 [Address user intent & questions]

Continue with logical flow of information.
Answer common questions users are searching for.

## Code Examples (if applicable)

```language
// Code examples should be well-commented
example code here
```

## Troubleshooting (if applicable)

[Great for targeting "how to fix..." searches]
Common issues and solutions.

## Conclusion

Summary of what was covered and next steps or related resources.
Include internal links to related articles.
```

**SEO BEST PRACTICES FOR CONTENT:**

**Keyword Optimization:**
- Use primary keyword in H1 title (automatically from front matter)
- Include primary keyword in first 100 words
- Use keyword naturally in 2-3 H2 headings
- Aim for 1-2% keyword density (natural usage)
- Use semantic variations and related terms
- Avoid keyword stuffing - prioritize readability

**Heading Structure (CRITICAL FOR SEO):**
- Use ONE H1 per article (the title)
- Use H2 for main sections (## in markdown)
- Use H3 for subsections (### in markdown)
- Make headings descriptive and keyword-rich
- Think: "What would users search for?"
- Examples:
  - Good: "How to Set Up GitHub Integration in 5 Minutes"
  - Bad: "Setup Process"
  - Good: "Troubleshooting Common Authentication Errors"
  - Bad: "Problems"

**Content Length & Quality:**
- Aim for 800-2000+ words for comprehensive topics
- Longer content ranks better IF it adds value
- Cover the topic thoroughly
- Answer related questions users might have
- Include examples and specific details

**Internal Linking:**
- Link to 2-5 related articles within content
- Use descriptive anchor text (not "click here")
- Helps with topic clustering and SEO authority
- Example: "Learn more about [setting up webhooks](../webhooks-guide)"

**Readability (AFFECTS SEO):**
- Use short paragraphs (2-4 sentences)
- Include bullet points and lists
- Add subheadings every 200-300 words
- Use bold for important terms
- Keep sentences concise
- Better readability = better engagement = better SEO

## Step 5: Add SEO-Optimized Images and Assets

**Storage:** Place all images directly in the article folder alongside the markdown files.

**Supported formats:** PNG, JPG, GIF, SVG

**Usage in markdown:**
```markdown
![Descriptive alt text with keywords](./keyword-descriptive-filename.png)
```

**IMAGE SEO BEST PRACTICES (CRITICAL):**

**File Names (IMPORTANT FOR IMAGE SEO):**
- Use descriptive, keyword-rich filenames
- Include target keywords when relevant
- Use hyphens to separate words
- Be specific about what the image shows
- Examples:
  - Good: `github-integration-dashboard-setup.png`
  - Bad: `img1.png`, `screenshot.png`
  - Good: `authentication-error-fix-settings.png`
  - Bad: `error.png`

**Alt Text (CRITICAL FOR SEO & ACCESSIBILITY):**
- ALWAYS include descriptive alt text
- Include relevant keywords naturally
- Describe what the image shows
- Keep it under 125 characters
- Think: "How would I describe this to someone who can't see it?"
- Examples:
  - Good: `![GitHub integration settings dashboard showing API key configuration](./github-dashboard-setup.png)`
  - Bad: `![Screenshot](./screenshot.png)`
  - Good: `![Authentication error message in JoAi settings panel](./auth-error.png)`
  - Bad: `![Error](./error.png)`

**Image Optimization:**
- Compress images before adding (use tools like TinyPNG)
- Keep file sizes under 500KB when possible
- Use appropriate dimensions (don't upload 4K images for small displays)
- Use SVG for diagrams and illustrations when possible (scalable and small)
- Optimized images = faster page load = better SEO

**SEO Benefits of Proper Image Optimization:**
- Images appear in Google Image Search
- Alt text helps with accessibility and SEO
- Faster load times improve page rankings
- Descriptive filenames help search engines understand content

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

## Step 8: SEO & Quality Validation Checklist

Before committing, verify ALL of these SEO-critical items:

**SEO Front Matter Checklist:**
- [ ] Title includes primary keyword
- [ ] Title is under 60 characters
- [ ] Description is 120-160 characters (not shorter, not longer)
- [ ] Description includes primary keyword
- [ ] Description has compelling value proposition
- [ ] Keywords field has 5-10 relevant search terms
- [ ] Primary keyword is first in keywords array
- [ ] llmAnswer field is completed with specific, direct answer
- [ ] FAQs section has 3-5 questions targeting long-tail searches
- [ ] relatedArticles links to 2-4 related content pieces
- [ ] Category is valid (ai, automation, integrations, blockchain, troubleshooting)
- [ ] Tags are specific and relevant (3-5 tags)
- [ ] Dates are in YYYY-MM-DD format

**Content SEO Checklist:**
- [ ] Primary keyword appears in first 100 words
- [ ] Primary keyword used naturally throughout (1-2% density)
- [ ] 2-3 H2 headings include keyword variations
- [ ] Headings are descriptive and keyword-rich
- [ ] Only ONE H1 heading (the title)
- [ ] Content is 800+ words (for comprehensive topics)
- [ ] Internal links to 2-5 related articles
- [ ] Internal links use descriptive anchor text
- [ ] Content answers user search intent
- [ ] Paragraphs are short and scannable
- [ ] Bullet points and lists used for readability
- [ ] Important terms are bolded

**Image SEO Checklist:**
- [ ] All image filenames are descriptive and keyword-rich
- [ ] All images have descriptive alt text with keywords
- [ ] Alt text is under 125 characters
- [ ] Images use relative paths (./image.png)
- [ ] Images are optimized/compressed
- [ ] No generic filenames (img1.png, screenshot.png, etc.)

**Technical Checklist:**
- [ ] Front matter has proper YAML delimiters (---)
- [ ] Markdown syntax is correct
- [ ] Code examples are properly formatted
- [ ] No broken links (internal or external)
- [ ] File is saved as article.en.md (or appropriate locale)

**AI Search Discovery Checklist:**
- [ ] llmAnswer provides direct, specific answer
- [ ] FAQs target common search queries
- [ ] Content structure is clear and logical for AI parsing
- [ ] Key information is stated explicitly (not just implied)

## Example Workflow: SEO-Optimized Article

Here's an example demonstrating SEO best practices:

```bash
# 1. Create directory with keyword-rich slug
mkdir -p articles/integrations/zapier-integration-guide

# 2. Create SEO-optimized article
cat > articles/integrations/zapier-integration-guide/article.en.md << 'EOF'
---
title: 'Connect JoAi to Zapier - Complete Setup Guide'
description: 'Set up Zapier integration with JoAi in 5 minutes. Automate workflows across 5,000+ apps using webhooks and API. Step-by-step tutorial with screenshots.'
category: 'integrations'
tags: ['zapier', 'integration', 'automation', 'webhooks', 'api']
author: 'JoAi Team'
publishedAt: '2026-01-04'
updatedAt: '2026-01-04'
keywords: ['zapier integration', 'connect zapier joai', 'zapier setup', 'automation workflows', 'webhook integration', 'api connection', 'zapier tutorial']
difficulty: 'beginner'
readTime: 8
relatedArticles: ['webhook-setup', 'api-authentication', 'automation-best-practices']
llmAnswer: 'Connect JoAi to Zapier via Settings > Integrations using webhooks or API. Setup takes 5 minutes and enables automation with 5,000+ apps like Gmail, Slack, and Google Sheets.'
faqs:
  - question: 'How long does Zapier setup take with JoAi?'
    answer: 'Setup takes approximately 5 minutes following the step-by-step guide.'
  - question: 'Do I need a paid Zapier account?'
    answer: 'No, the free Zapier plan works with JoAi, though paid plans offer more features.'
  - question: 'What apps can I connect through Zapier?'
    answer: 'Over 5,000 apps including Gmail, Slack, Google Sheets, Trello, and Salesforce.'
  - question: 'Should I use webhooks or API for integration?'
    answer: 'Webhooks are recommended for real-time triggers, while API works for batch operations.'
---

# Connect JoAi to Zapier - Complete Setup Guide

Connecting JoAi to Zapier lets you automate workflows across 5,000+ applications without coding. This guide walks you through the setup process using webhooks and API connections in just 5 minutes.

## What You'll Learn

- How to connect your JoAi account to Zapier
- Setting up webhooks and API authentication
- Creating your first automated workflow
- Troubleshooting common connection issues

## Setting Up the Integration

### Access Integration Settings

In your JoAi dashboard, navigate to Settings > Integrations...

[Content continues with proper structure, natural keyword usage]
EOF

# 3. Add images with SEO-friendly names
# Examples:
# - zapier-integration-dashboard.png
# - webhook-configuration-screen.png
# - api-setup-tutorial.png

# Use descriptive alt text:
# ![JoAi integration settings showing Zapier connection options](./zapier-integration-dashboard.png)
```

**Key SEO elements demonstrated:**
- Keyword-rich slug, title, and description
- Natural keyword usage (not stuffed)
- Comprehensive keywords array
- Strong llmAnswer for AI search
- FAQs targeting common searches
- Descriptive image filenames and alt text

## Tips for SEO-Optimized, High-Quality Articles

1. **Start with keyword research** - What are users actually searching for?
2. **Front-load keywords** - Put important keywords in titles, URLs, and first paragraph
3. **Answer search intent** - Understand WHY users search and deliver that answer
4. **Use examples** - Real-world scenarios help understanding AND SEO engagement
5. **Include screenshots** - Visual aids improve comprehension and time-on-page
6. **Optimize every image** - Keyword-rich filenames and alt text boost image search traffic
7. **Keep it scannable** - Use headings, bullets, and short paragraphs (better engagement = better SEO)
8. **Add FAQs** - Target featured snippets and long-tail searches
9. **Complete llmAnswer** - Maximize AI search discovery (ChatGPT, Claude, Perplexity)
10. **Add troubleshooting** - Captures "how to fix..." search traffic
11. **Link related content** - Internal linking builds topic authority
12. **Write comprehensive content** - 800-2000+ words for competitive keywords
13. **Optimize for readability** - Short sentences, clear language (affects engagement metrics)
14. **Test your content** - Follow your own instructions to verify accuracy
15. **Update regularly** - Fresh content ranks better; update the updatedAt field

## Common SEO Mistakes to Avoid

**Critical SEO Errors:**
- Don't skip the llmAnswer field - it's critical for AI search discovery
- Don't write vague titles - always include your target keyword
- Don't write short descriptions - 120-160 characters is the SEO sweet spot
- Don't use generic image names - "screenshot.png" has zero SEO value
- Don't skip image alt text - you're missing image search traffic
- Don't stuff keywords unnaturally - it hurts readability and rankings
- Don't write thin content - aim for 800+ words on competitive topics
- Don't ignore search intent - answer what users are actually looking for
- Don't skip FAQs - you're missing featured snippet opportunities
- Don't forget internal links - they build topic authority
- Don't use vague headings - make them descriptive and keyword-rich

**Technical Errors:**
- Don't forget the front matter YAML delimiters (---)
- Don't use absolute image paths - always use relative paths
- Don't exceed character limits for title (60) and description (160)
- Don't use invalid category names
- Don't forget to update the updatedAt date when editing
- Don't create articles without the .en.md suffix for English
- Don't use generic slugs without keywords

## SEO Strategy Overview

When creating articles, follow this SEO-first approach:

**1. Keyword Research First:**
- Identify what users are actually searching for
- Use tools like Google Autocomplete, "People also ask", etc.
- Choose a primary keyword with search volume
- Identify 3-5 secondary/related keywords

**2. Understand Search Intent:**
- Informational: "what is", "how does" → Provide explanations
- Navigational: "login", "dashboard" → Provide directions
- Transactional: "setup", "integrate" → Provide step-by-step guides
- Problem-solving: "fix", "troubleshoot" → Provide solutions

**3. Optimize for Both Engines:**
- **Traditional SEO** (Google, Bing):
  - Keywords in title, URL, headings, first paragraph
  - 120-160 char descriptions
  - Internal linking
  - Image optimization
  - Content length (800+ words)

- **AI Search** (ChatGPT, Claude, Perplexity):
  - Complete llmAnswer with direct answer
  - Well-structured FAQs
  - Clear, explicit statements (not just implied)
  - Comprehensive coverage of topic

**4. Content Structure for Maximum Discovery:**
- Keyword-rich title (H1)
- Keyword in first 100 words
- Descriptive H2/H3 headings with keywords
- FAQs targeting long-tail searches
- Internal links to related content
- Troubleshooting section (captures problem queries)
- Clear, direct answers to questions

**5. Measure Success:**
- Monitor which articles get traffic
- Update content that's not performing
- Refresh outdated information (update updatedAt)
- Add more keywords/FAQs to successful articles
- Build content clusters around popular topics

## Integration with Git

All articles are version-controlled in Git. After creating or editing:

```bash
git add articles/
git commit -m "Add article: [Article Title]"
git push
```

The knowledge base automatically syncs with the JoAi app through GitHub integration.

## Quick Reference: SEO Checklist

Use this quick checklist when creating articles:

1. **Slug** → Contains primary keyword
2. **Title** → Under 60 chars, includes keyword
3. **Description** → 120-160 chars, includes keyword + value prop
4. **Keywords** → 5-10 terms, primary keyword first
5. **llmAnswer** → Direct 1-2 sentence answer for AI search
6. **FAQs** → 3-5 questions targeting long-tail searches
7. **First paragraph** → Includes keyword within 100 words
8. **Headings** → Descriptive, keyword-rich H2/H3 headings
9. **Content length** → 800+ words for comprehensive topics
10. **Images** → Keyword-rich filenames + descriptive alt text
11. **Internal links** → 2-5 links to related articles
12. **relatedArticles** → 2-4 article slugs in front matter

## Need Help?

- Check existing articles in `articles/` for examples
- Review the template in `templates/article-template.md`
- See the main README.md for more information
- Focus on SEO from the start - it's easier than retrofitting later
