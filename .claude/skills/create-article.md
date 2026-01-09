# Create Knowledge Base Article

This skill teaches you how to create SEO-optimized articles for the JoAi Knowledge Base.

## Overview

The JoAi Knowledge Base is a document-based system where articles are stored as Markdown files with YAML front matter. Articles are organized by category and slug, support multiple languages, and can include images and other assets.

**PRIMARY GOAL: MAXIMIZE SEO, AI SEARCH DISCOVERY & READER ENGAGEMENT** - Every article must be optimized for:
1. **Traditional Search Engines** (Google, Bing) - Drive organic traffic through keyword optimization
2. **AI Search Systems** (ChatGPT, Claude, Perplexity) - Ensure AI assistants can discover and cite your content
3. **Reader Engagement** - Use effective copywriting to keep readers engaged and wanting more

SEO and AI discoverability get users to your content. Effective copywriting keeps them reading and coming back for more. These considerations should guide ALL decisions from slug selection to content structure.

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

## Step 2: Analyze Existing Articles for Style and Format

**CRITICAL: Before creating your article, scan the repository to understand the established writing style, tone, and format.**

This ensures consistency across the knowledge base and helps you match the existing voice and structure.

### Scan the Repository

Use the Glob tool to find existing articles in the same category:
```bash
# Example: Find all articles in the integrations category
articles/integrations/**/article.en.md
```

### Read 2-3 Example Articles

Select and read 2-3 recent or similar articles from the repository. Pay close attention to:

**Writing Style & Tone:**
- **Formality level** - Is it casual and conversational, or more professional and formal?
- **Person perspective** - Does it use "you" (second person), "we" (first person plural), or avoid pronouns?
- **Sentence structure** - Are sentences short and punchy, or longer and more detailed?
- **Technical depth** - How much technical jargon is used? Is it beginner-friendly or assumes knowledge?
- **Voice consistency** - Is the tone consistent throughout, or does it shift between sections?

**Format Patterns:**
- **Section organization** - What sections are commonly included? (e.g., "What You'll Learn", "Troubleshooting", "Best Practices")
- **Heading structure** - How are H2 and H3 headings used? What naming patterns are common?
- **Code examples** - How are code blocks formatted? How much explanation surrounds them?
- **Lists and bullets** - When are bulleted lists used vs. numbered lists?
- **Callouts and emphasis** - How is important information highlighted? (bold, italics, blockquotes)

**Content Structure:**
- **Introduction pattern** - How do articles typically start? What information is in the first paragraph?
- **Step-by-step guides** - How are sequential instructions formatted?
- **Examples and use cases** - Where are examples placed? How detailed are they?
- **Visual aids** - How often are images used? What types of screenshots are included?
- **Conclusion pattern** - How do articles wrap up? What's included in the final section?

**Specific Elements to Note:**
- **Keyword usage** - How naturally are keywords woven into the text? How often are they repeated?
- **Link placement** - Where do internal and external links appear?
- **FAQs structure** - How are questions phrased? How detailed are answers?
- **Code comments** - How are code examples commented and explained?
- **Transition phrases** - What phrases connect sections? ("Now that...", "Next...", "Here's how...")

### Apply the Observed Style

When writing your new article:
1. **Match the tone** - Use the same level of formality and conversational style
2. **Follow structural patterns** - Include similar sections and organization
3. **Mirror formatting** - Use the same heading styles, list formats, and emphasis patterns
4. **Adopt phrasing patterns** - Use similar transition phrases and explanatory language
5. **Maintain consistency** - Your article should feel like it belongs in the same collection

### Example Analysis Workflow

```markdown
# After reading articles/integrations/github-integration/article.en.md

Observed patterns:
- Tone: Conversational and friendly ("You'll need", "Here's how")
- Uses second person ("you", "your") consistently
- Short paragraphs (2-4 sentences)
- Includes "What You'll Learn" section early
- Heavy use of H3 subheadings for organization
- Code examples with brief explanations
- Extensive troubleshooting section
- Ends with "Conclusion" and next steps
- Uses bold for important terms on first mention
- Includes practical examples throughout

→ Apply these same patterns to your new article
```

**Important Notes:**
- If articles in the repository have varying styles, choose the most recent ones as they likely represent the current standard
- If you're creating an article for a new category with no examples, use articles from similar categories as reference
- Don't just copy structure - understand WHY certain patterns work and adapt them to your specific topic
- Consistency is key for user experience and SEO performance

## Step 3: Create Article Directory

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

## Step 5: Write SEO-Optimized, Engaging Article Content

**Remember to apply the style and tone patterns you observed in Step 2!**

After the front matter, structure your content for maximum SEO impact AND reader engagement. Great articles don't just rank well—they keep readers hooked from start to finish.

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

### Copywriting for Reader Engagement

**CRITICAL: SEO gets readers to your article. Copywriting keeps them reading.**

Great technical writing isn't just informative—it's engaging. These copywriting principles ensure readers stay hooked and come back for more articles.

**Hook Your Reader Immediately:**
- Open with a compelling first sentence that creates curiosity or addresses a pain point
- State the benefit or transformation the reader will get
- Make readers feel "this article is exactly what I needed"
- Examples:
  - Good: "Stop wrestling with authentication errors—here's the fix that works every time."
  - Bad: "This article covers authentication errors."
  - Good: "In 5 minutes, you'll have a Zapier integration that saves you hours of manual work."
  - Bad: "This guide explains Zapier integration."

**Write for Scanners First, Readers Second:**
- Most readers scan before committing to read
- Use clear subheadings that tell a story on their own
- Front-load each paragraph with the key point
- Use bullet points to break up dense information
- Bold the most important phrases (readers' eyes go there first)

**Use the "So What?" Test:**
- After every statement, ask "so what?" or "why should the reader care?"
- Connect features to benefits
- Examples:
  - Feature: "The API supports webhooks"
  - So what?: "...so you get real-time updates without constantly polling"
  - Feature: "Setup takes 5 minutes"
  - So what?: "...which means you can start automating today, not next week"

**Create Momentum with Transitions:**
- Guide readers smoothly from section to section
- Use transitional phrases that create anticipation:
  - "Now that you've set up the basics, here's where it gets interesting..."
  - "But here's the part most people miss..."
  - "Ready for the next step? Let's tackle..."
  - "Here's the secret to making this actually work..."
- Avoid abrupt section changes that lose reader attention

**Write Like You're Talking to a Friend:**
- Use "you" and "your" to make it personal
- Write in a conversational tone (but stay professional)
- Address the reader's situation directly
- Examples:
  - Good: "You've probably hit this error before. Here's why it happens."
  - Bad: "Users may encounter this error. The cause is documented below."

**Use Specific Numbers and Details:**
- Specificity builds credibility and interest
- Examples:
  - Good: "This method reduced our API calls by 73%"
  - Bad: "This method significantly reduces API calls"
  - Good: "Complete setup in 5 minutes with 3 simple steps"
  - Bad: "Quick and easy setup process"

**Create "Aha!" Moments:**
- Include insights that make readers feel smarter
- Share non-obvious tips or shortcuts
- Explain the "why" behind the "what"
- Examples:
  - "Here's something most tutorials don't tell you..."
  - "The reason this works is..."
  - "Pro tip: You can skip steps 2-4 if..."

**Handle Objections Proactively:**
- Anticipate reader doubts or concerns
- Address them before they become roadblocks
- Examples:
  - "You might be thinking 'this sounds complicated'—but watch how simple it actually is."
  - "Don't worry if you're not technical. This guide assumes zero prior knowledge."
  - "Yes, this works with the free plan too."

**End Sections with Forward Motion:**
- Don't let readers' attention fade at section breaks
- End each section with a hook to the next
- Create a sense of progress and momentum
- Examples:
  - "With authentication sorted, you're ready for the fun part: building your first workflow."
  - "That's the foundation. Now let's see how to customize it for your specific needs."

**Write Compelling Conclusions:**
- Summarize what the reader accomplished (reinforce their progress)
- Suggest clear next steps or related articles
- End on an empowering note
- Examples:
  - Good: "You now have a fully automated workflow that will save you hours every week. Next, check out our [advanced triggers guide] to take it even further."
  - Bad: "This concludes the integration guide."

**Copywriting Patterns to Avoid:**
- Wall-of-text paragraphs (readers bounce immediately)
- Passive voice overuse ("the button should be clicked" → "click the button")
- Jargon without explanation (alienates beginners)
- Burying the lead (put key info first, context second)
- Generic opening sentences ("In this article, we will discuss...")
- Unnecessary hedge words ("perhaps", "maybe", "might", "somewhat")
- Over-qualifying statements (just say it confidently)

**The AIDA Framework for Introductions:**
Use this classic copywriting framework for article intros:
1. **Attention**: Hook with a compelling opening
2. **Interest**: Present the problem or opportunity
3. **Desire**: Show the benefits of reading further
4. **Action**: Tell them what they'll be able to do

Example intro using AIDA:
```markdown
Stop copying data between apps manually. [Attention]

If you're spending hours each week on repetitive tasks that could be automated,
you're not alone—and there's a better way. [Interest]

This guide shows you how to connect JoAi to Zapier in 5 minutes,
giving you access to 5,000+ app integrations that run automatically. [Desire]

By the end, you'll have your first automated workflow up and running. [Action]
```

**Voice and Tone Guidelines:**
- **Be helpful, not preachy**: Guide, don't lecture
- **Be confident, not arrogant**: Share expertise without talking down
- **Be friendly, not unprofessional**: Warm but credible
- **Be concise, not terse**: Clear and efficient, but not cold
- **Be honest about limitations**: Readers trust transparency

## Step 6: Add SEO-Optimized Images and Assets

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

## Step 7: Create Localized Versions (Optional)

To add additional language support:

1. Copy the English version
2. Create a new file with the locale code: `article.de.md`, `article.fr.md`, etc.
3. Translate all content (both front matter and body)
4. Keep the same slug and directory structure
5. Use the same image references (images are shared across locales)

## Step 8: Reference the Template

A complete template is available at:
```
templates/article-template.md
```

Use this as a starting point for consistency.

## Step 9: SEO & Quality Validation Checklist

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

**Style Consistency Checklist (from Step 2):**
- [ ] Tone matches existing articles in the category
- [ ] Uses same person perspective (e.g., second person "you")
- [ ] Paragraph length is consistent with repository style
- [ ] Section organization follows established patterns
- [ ] Heading naming conventions match existing articles
- [ ] Transition phrases and language patterns are consistent
- [ ] Code examples formatted like existing articles
- [ ] Emphasis and callouts match repository style

**Copywriting & Reader Engagement Checklist:**
- [ ] Opening sentence hooks the reader (addresses pain point or creates curiosity)
- [ ] First paragraph uses AIDA framework (Attention, Interest, Desire, Action)
- [ ] Benefits are stated, not just features ("so you can..." not just "it does...")
- [ ] Paragraphs are front-loaded with key information
- [ ] Transitions between sections create momentum
- [ ] Uses "you" and "your" consistently (personal address)
- [ ] Specific numbers and details used instead of vague claims
- [ ] No wall-of-text paragraphs (2-4 sentences max)
- [ ] Key phrases are bolded for scanners
- [ ] Objections and doubts are proactively addressed
- [ ] Includes "aha!" moments or non-obvious insights
- [ ] Each section ends with forward motion to next section
- [ ] Conclusion summarizes accomplishment and suggests next steps
- [ ] No passive voice overuse
- [ ] No generic opening sentences ("In this article, we will...")
- [ ] Voice is helpful and confident, not preachy or condescending

## Example Workflow: SEO-Optimized, Engaging Article

Here's an example demonstrating SEO best practices AND effective copywriting:

```bash
# 1. Choose category and keyword-rich slug
# Category: integrations
# Slug: zapier-integration-guide

# 2. Analyze existing articles for style
# Find existing articles in the integrations category
# Read 2-3 articles to understand tone, format, and structure patterns
# Note: Conversational tone, "you" perspective, includes "What You'll Learn",
#       extensive troubleshooting, uses H3 subheadings, ends with Conclusion

# 3. Create directory with keyword-rich slug
mkdir -p articles/integrations/zapier-integration-guide

# 4. Create SEO-optimized article (applying observed style patterns)
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

Stop copying data between apps manually—there's a better way. [HOOK - addresses pain point]

If you're spending hours each week on repetitive tasks, you're not alone. This guide shows you how to connect JoAi to Zapier in just 5 minutes, unlocking 5,000+ app integrations that run automatically while you focus on what matters. [AIDA - Interest/Desire]

By the end, you'll have your first automated workflow up and running. [AIDA - Action]

## What You'll Learn

- How to connect your JoAi account to Zapier (takes about 2 minutes)
- Setting up webhooks and API authentication the right way
- Creating your first automated workflow that actually saves time
- Troubleshooting tips so you don't get stuck

## Setting Up the Integration

Here's something most tutorials skip: there are two ways to connect JoAi to Zapier, and picking the right one saves you headaches later. [AHA MOMENT]

### Access Integration Settings

In your JoAi dashboard, navigate to Settings > Integrations...

[Content continues with engaging transitions between sections]

With authentication sorted, you're ready for the fun part—building your first workflow. [FORWARD MOTION]
EOF

# 5. Add images with SEO-friendly names
# Examples:
# - zapier-integration-dashboard.png
# - webhook-configuration-screen.png
# - api-setup-tutorial.png

# Use descriptive alt text:
# ![JoAi integration settings showing Zapier connection options](./zapier-integration-dashboard.png)
```

**Key SEO elements demonstrated:**
- Analyzed existing articles for style consistency (Step 2)
- Keyword-rich slug, title, and description
- Natural keyword usage (not stuffed)
- Comprehensive keywords array
- Strong llmAnswer for AI search
- FAQs targeting common searches
- Descriptive image filenames and alt text
- Consistent tone and format with existing articles

**Key copywriting elements demonstrated:**
- Opening hook that addresses reader pain point
- AIDA framework in introduction (Attention, Interest, Desire, Action)
- "What You'll Learn" items include specific benefits
- "Aha!" moment sharing non-obvious insight
- Forward motion transition to next section
- Conversational "you" language throughout
- Specific numbers (5 minutes, 5,000+ apps) instead of vague claims

## Tips for SEO-Optimized, Engaging Articles

**SEO & Discovery:**
1. **Analyze existing articles first** - Understand the established style, tone, and format before writing
2. **Start with keyword research** - What are users actually searching for?
3. **Front-load keywords** - Put important keywords in titles, URLs, and first paragraph
4. **Answer search intent** - Understand WHY users search and deliver that answer
5. **Optimize every image** - Keyword-rich filenames and alt text boost image search traffic
6. **Add FAQs** - Target featured snippets and long-tail searches
7. **Complete llmAnswer** - Maximize AI search discovery (ChatGPT, Claude, Perplexity)
8. **Add troubleshooting** - Captures "how to fix..." search traffic
9. **Link related content** - Internal linking builds topic authority
10. **Write comprehensive content** - 800-2000+ words for competitive keywords
11. **Update regularly** - Fresh content ranks better; update the updatedAt field

**Copywriting & Engagement:**
12. **Hook readers in the first sentence** - Address a pain point or create curiosity immediately
13. **Use the AIDA framework** - Attention, Interest, Desire, Action for introductions
14. **Write for scanners** - Use clear headings, bullets, and bold key phrases
15. **Connect features to benefits** - Always answer "so what?" for the reader
16. **Create forward motion** - End sections with hooks to keep readers moving forward
17. **Include "aha!" moments** - Share non-obvious insights that make readers feel smarter
18. **Address objections proactively** - Anticipate and resolve reader doubts
19. **Use specific numbers** - "5 minutes" beats "quick setup" every time
20. **Write like you're helping a friend** - Conversational but professional
21. **End with empowerment** - Summarize what readers accomplished and what's next

**Quality & Readability:**
22. **Use examples** - Real-world scenarios help understanding AND engagement
23. **Include screenshots** - Visual aids improve comprehension and time-on-page
24. **Keep it scannable** - Use headings, bullets, and short paragraphs
25. **Optimize for readability** - Short sentences, clear language, no jargon without explanation
26. **Test your content** - Follow your own instructions to verify accuracy

## Common Mistakes to Avoid

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

**Copywriting & Engagement Errors:**
- Don't start with "In this article, we will discuss..." - hook readers immediately instead
- Don't write wall-of-text paragraphs - readers bounce immediately
- Don't use passive voice ("the button should be clicked") - use active voice ("click the button")
- Don't just list features - connect them to reader benefits ("so you can...")
- Don't end sections abruptly - create momentum to the next section
- Don't use vague claims ("very fast") - use specific numbers ("loads in 0.3 seconds")
- Don't ignore reader objections - address doubts proactively
- Don't use jargon without explanation - you'll lose non-expert readers
- Don't be preachy or condescending - guide, don't lecture
- Don't bury the lead - put key information first in each section
- Don't forget the conclusion - summarize accomplishments and empower readers
- Don't overuse hedge words ("perhaps", "maybe", "might") - be confident

**Technical Errors:**
- Don't forget the front matter YAML delimiters (---)
- Don't use absolute image paths - always use relative paths
- Don't exceed character limits for title (60) and description (160)
- Don't use invalid category names
- Don't forget to update the updatedAt date when editing
- Don't create articles without the .en.md suffix for English
- Don't use generic slugs without keywords

## Content Strategy Overview

When creating articles, follow this SEO + copywriting approach:

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

**5. Write for Engagement (Copywriting):**
- Hook readers in the first sentence (pain point or curiosity)
- Use AIDA framework for introductions
- Connect features to benefits throughout
- Create momentum with transitions between sections
- Include "aha!" moments and non-obvious insights
- Address objections before they become roadblocks
- End with empowerment and clear next steps
- Write like you're helping a friend

**6. Measure Success:**
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

## Quick Reference: Complete Checklist

Use this quick checklist when creating articles:

**SEO Essentials:**
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

**Copywriting Essentials:**
13. **Opening hook** → First sentence addresses pain point or creates curiosity
14. **AIDA intro** → Attention, Interest, Desire, Action in introduction
15. **Benefits over features** → Answer "so what?" for everything
16. **Forward motion** → Transitions between sections keep readers engaged
17. **Specific numbers** → Use concrete details, not vague claims
18. **Personal address** → Use "you" and "your" consistently
19. **Short paragraphs** → 2-4 sentences max, no walls of text
20. **Empowering conclusion** → Summarize accomplishment, suggest next steps

## Need Help?

- Check existing articles in `articles/` for examples
- Review the template in `templates/article-template.md`
- See the main README.md for more information
- Focus on SEO from the start - it's easier than retrofitting later
