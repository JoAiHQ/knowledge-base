---
title: 'GitHub Integration Guide for JoAi'
description: 'Set up GitHub integration with JoAi in 5 minutes. Create issues, manage pull requests, search repositories, and automate workflows using GitHub REST API v3. Complete setup guide.'
category: 'integrations'
tags: ['github', 'integration', 'api', 'automation', 'version-control']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
draft: true
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['github integration', 'github integration setup', 'connect github joai', 'github api integration', 'github automation', 'github workflow automation', 'github rest api', 'github personal access token', 'github issues api', 'github pull requests']
relatedArticles: []
faqs:
  - question: 'How long does GitHub integration setup take?'
    answer: 'Setup takes approximately 5 minutes. You need to create a Personal Access Token and set it as an environment variable.'
  - question: 'What permissions does the GitHub integration need?'
    answer: 'The integration requires a Personal Access Token with the `repo` scope for full functionality. Additional scopes like `read:org` and `read:user` may be needed for organization repositories.'
  - question: 'Can I use this integration with private repositories?'
    answer: 'Yes, as long as your Personal Access Token has the `repo` scope, you can access and manage private repositories.'
  - question: 'What is the rate limit for GitHub API requests?'
    answer: 'Authenticated requests have a rate limit of 5,000 requests per hour. Unauthenticated requests are limited to 60 requests per hour.'
  - question: 'How do I create a cross-repository pull request?'
    answer: 'Use the format `username:branch-name` for the Head Branch field when creating a pull request from a fork or different repository.'
llmAnswer: 'Set up GitHub integration in JoAi by creating a Personal Access Token with the `repo` scope and setting it as the GITHUB_TOKEN environment variable. This enables creating issues, pull requests, adding comments, and searching repositories via GitHub REST API v3.'
---

The GitHub integration for JoAi lets you manage your GitHub repositories, issues, and pull requests directly from your workspace. This GitHub integration uses GitHub's REST API v3, so you can automate your GitHub workflow without leaving JoAi. Setting up the GitHub integration takes just 5 minutes and unlocks powerful automation capabilities.

## What You'll Learn

* How to set up GitHub integration with Personal Access Tokens
* Creating and managing GitHub issues and pull requests
* Searching repositories using GitHub's search syntax
* Adding comments to issues and PRs
* Troubleshooting common GitHub integration errors
* Best practices for GitHub API authentication and security

## How to Set Up GitHub Integration

You'll need a GitHub Personal Access Token to use this GitHub integration. Here's how to set it up in just a few minutes.

### Create Your GitHub Personal Access Token

Head over to [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens) and click **"Generate new token"** → **"Generate new token (classic)"**.

Give it a name like "JoAi Integration" and set an expiration (we recommend 90 days). For **GitHub integration scopes**, you'll need:

* **`repo`** - This gives you full control of private repositories. You'll need this for most GitHub integration operations like creating issues and PRs.
* **`read:org`** - Only if you're working with organization repositories
* **`read:user`** - For reading user profile data

Click **"Generate token"** and copy it immediately. GitHub won't show it to you again.

### Configure GitHub Integration Environment Variable

Set the `GITHUB_TOKEN` environment variable with your **GitHub Personal Access Token**:

**macOS/Linux:**
```bash
export GITHUB_TOKEN="your_token_here"
```

To make it stick, add it to your `~/.zshrc` or `~/.bashrc`:
```bash
echo 'export GITHUB_TOKEN="your_token_here"' >> ~/.zshrc
source ~/.zshrc
```

**Windows (PowerShell):**
```powershell
$env:GITHUB_TOKEN="your_token_here"
```

**Windows (Command Prompt):**
```cmd
setx GITHUB_TOKEN "your_token_here"
```

**Docker:**
```bash
docker run -e GITHUB_TOKEN="your_token_here" ...
```

### Verify GitHub Integration Setup

Try the "Get Repository" warp with a public repo to verify your **GitHub integration** works:

* Owner: `octocat`
* Repository: `Hello-World`

If you see repository info with stars and forks, you're all set.

## GitHub Integration Features and Actions

### Create GitHub Issues

Use the `github/create-issue` warp to create a new **GitHub issue** in any repository through the GitHub integration.

You'll need:
* Owner (username or org)
* Repository name
* Title
* Body (optional, supports Markdown)
* Labels (optional, comma-separated like "bug,enhancement")
* Assignees (optional, comma-separated usernames)

You'll get back the issue number, URL, and GitHub's internal ID.

Here's an example:
```
Owner: myusername
Repository: myproject
Title: Fix login bug
Body: The login form is not validating email addresses correctly.
Labels: bug,priority-high
Assignees: developer1,developer2
```

### Get GitHub Repository Information

The `github/get-repository` warp gives you all the details about any **GitHub repository** through the integration.

Just provide the owner and repository name. You'll get back the name, description, stars, forks, language, and clone URLs.

```
Owner: facebook
Repository: react
```

### List GitHub Issues

Use `github/list-issues` to list **GitHub issues** in a repo through the integration. You can filter by state (`open`, `closed`, or `all`), labels, assignee, and limit results (max 100, default 30).

You'll get an array of issues and the total count.

```
Owner: myusername
Repository: myproject
State: open
Labels: bug
Assignee: developer1
Limit: 50
```

### Get Specific GitHub Issue Details

The `github/get-issue` warp pulls all the details for a single **GitHub issue** - title, body, state, labels, assignees, and author.

```
Owner: myusername
Repository: myproject
Issue Number: 42
```

### Create GitHub Pull Requests

The `github/create-pull-request` warp creates a new **GitHub pull request** to merge changes between branches through the integration.

You'll need the owner, repo, title, head branch (source), and base branch (target, usually `main`). For cross-repo PRs, use `username:branch` format for the head branch. Set `Draft: true` if you want a draft PR.

You'll get back the PR number, URL, and state.

```
Owner: myusername
Repository: myproject
Title: Add user authentication
Body: Implements OAuth2 authentication flow with JWT tokens.
Head Branch: feature/auth
Base Branch: main
Draft: false
```

### Add Comments to GitHub Issues and PRs

Use `github/add-comment` to add a comment to any **GitHub issue or pull request** through the integration. The comment body supports Markdown.

You'll get back the comment ID and URL.

```
Owner: myusername
Repository: myproject
Issue Number: 42
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

### Search GitHub Repositories

The `github/search-repositories` warp lets you **search GitHub repositories** using their search syntax through the integration. You can sort by stars, forks, help-wanted-issues, or updated date, and limit results (max 100).

You'll get an array of matching repositories and the total count.

Some search query examples:
* `language:javascript stars:>100` - JavaScript repos with 100+ stars
* `topic:machine-learning` - Repos tagged with machine-learning
* `user:facebook` - All repos by Facebook
* `react in:name` - Repos with "react" in the name

```
Query: language:typescript stars:>500
Sort: stars
Order: desc
Limit: 50
```

## GitHub Integration Authentication

We use Personal Access Tokens (PATs) for GitHub integration authentication. It's the simplest way to connect to GitHub's API and manage your repositories.

### What scopes you need

For full functionality, your token needs the `repo` scope. This lets you create issues, pull requests, add comments, and access private repositories.

You'll also want `read:org` if you're working with organization repos, and `read:user` for user profile operations.

### Security tips

A few things to keep in mind:

* Set tokens to expire (90 days is a good default)
* Only grant the scopes you actually need
* Rotate tokens regularly
* Never commit tokens to version control
* Use environment variables or secret managers in production
* For org repos, consider fine-grained tokens or GitHub Apps

### Rate limits

GitHub limits authenticated requests to 5,000 per hour. Unauthenticated requests are capped at 60 per hour. You'll see rate limit info in response headers.

## How GitHub Integration Works

All GitHub integration requests go to `https://api.github.com` with your token in the Authorization header. We use GitHub's REST API v3, so everything follows their standard format.

Rate limit info comes back in response headers - you'll see how many requests you have left and when the limit resets. This GitHub integration handles all the API communication for you.

## GitHub Integration Use Cases and Examples

### Automated GitHub Issue Creation

Create a **GitHub issue** automatically when your app detects a bug using the GitHub integration:

```
Action: Create Issue
Owner: mycompany
Repository: myapp
Title: [BUG] Login validation failing
Body: ## Description
The login form is not validating email addresses correctly.

## Steps to Reproduce
1. Go to login page
2. Enter invalid email
3. Submit form

Labels: bug,priority-high
Assignees: backend-team
```

### Monitor GitHub Repository Statistics

Check how your **GitHub repository** is performing using the integration:

```
Action: Get Repository
Owner: myusername
Repository: myproject
```

Then look at the stars, forks, and language stats.

### GitHub Issue Triage Workflow

Filter **GitHub issues** to find what needs attention using the GitHub integration:

```
Action: List Issues
Owner: myusername
Repository: myproject
State: open
Labels: bug,needs-triage
Limit: 100
```

### Cross-Repository GitHub Pull Requests

Create a **GitHub pull request** from a fork using the `username:branch` format through the integration:

```
Action: Create Pull Request
Owner: upstream-org
Repository: upstream-repo
Title: Fix typo in README
Body: Fixed a typo in the installation instructions.
Head Branch: myusername:patch-1
Base Branch: main
```

### Find Trending GitHub Repositories

Search for popular **GitHub repositories** using the integration:

```
Action: Search Repositories
Query: language:rust stars:>1000 created:>2024-01-01
Sort: stars
Order: desc
Limit: 20
```

## Troubleshooting GitHub Integration Issues

### "Bad credentials" error

Your token isn't working. Check that:
* The `GITHUB_TOKEN` environment variable is set correctly
* The token hasn't expired
* The token has the required scopes

If all else fails, regenerate the token.

### "Not Found" error

GitHub can't find the repository or resource. Make sure:
* The owner and repository name are spelled correctly
* The repository actually exists
* For private repos, your token has the `repo` scope
* You have access to organization repositories if needed

### "Resource not accessible by integration" error

Your token doesn't have the right permissions. Regenerate it with the appropriate scopes. For organization repos, check your org settings too.

### Rate limit exceeded

You're hitting GitHub's rate limits. Wait for the reset (check the `X-RateLimit-Reset` header) or implement throttling in your app. Authenticated requests get 5,000 requests/hour, which should be plenty for most use cases.

### "Validation Failed" error

Something's wrong with your input. Check that:
* All required fields are provided
* Branch names and usernames are formatted correctly
* Labels actually exist in the repository
* Assignee usernames are valid

### Quick debugging tips

* Test with public repos first (like `octocat/Hello-World`) to verify your setup
* Double-check your token scopes
* Make sure all required fields are filled in
* Read the error messages - they usually tell you exactly what's wrong

## Best practices

### Token management

Use separate tokens for dev, staging, and production. Rotate them regularly, and store them securely in environment variables or secret managers. Fine-grained tokens are great if you can use them.

### Error handling

Always check for API errors in responses. Implement retry logic for rate limit errors, and log everything for debugging. Your users will thank you for clear error messages.

### Rate limiting

Keep an eye on rate limit headers. Use exponential backoff for retries, cache responses when you can, and batch operations when possible.

### Security

Never commit tokens to version control. Use `.gitignore` for environment files, restrict scopes to the minimum you need, and audit token usage regularly.

### Repository management

Keep naming consistent, document your repo structure, use labels effectively, and set up branch protection rules.

## Advanced usage

### Cross-repo pull requests

For PRs from forks or other repos, use `username:branch-name` format for the head branch.

### Markdown support

All text fields support GitHub Flavored Markdown - headers, lists, code blocks, task lists, tables, mentions (@username), and issue/PR references (#123).

### Webhooks

While not directly supported, you can combine GitHub webhooks with JoAi to automatically create issues, update issues from external triggers, or sync data between systems.

## Resources

* [GitHub REST API Docs](https://docs.github.com/en/rest)
* [GitHub API Authentication](https://docs.github.com/en/rest/authentication)
* [Personal Access Tokens](https://github.com/settings/tokens)
* [GitHub Search Syntax](https://docs.github.com/en/search-github/searching-on-github)
* [GitHub API Rate Limits](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
* [GitHub Flavored Markdown](https://github.github.com/gfm/)

---

## Conclusion

You're now ready to use the GitHub integration in JoAi! This GitHub integration enables you to automate your GitHub workflow, manage repositories, and streamline your development process. Start with simple operations like creating issues, then explore more advanced features like automated pull requests and repository searches.

Remember to keep your Personal Access Token secure, rotate it regularly, and monitor your API rate limits. For more advanced automation, consider combining this GitHub integration with webhooks and other JoAi features. Explore other JoAi integrations to build comprehensive automation workflows.

**Note**: This GitHub integration uses GitHub REST API v3. We're considering adding GraphQL API v4 support in the future.
