---
title: 'GitHub Integration Guide'
description: 'Learn how to set up and use the GitHub integration in Warpbase. Create issues, manage pull requests, search repositories, and automate your GitHub workflow.'
category: 'integrations'
tags: ['github', 'integration', 'api', 'automation', 'version-control']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['github', 'git', 'repository', 'issues', 'pull requests', 'api', 'automation']
relatedArticles: []
faqs:
  - question: 'What permissions does the GitHub integration need?'
    answer: 'The integration requires a Personal Access Token with the `repo` scope for full functionality. Additional scopes like `read:org` and `read:user` may be needed for organization repositories.'
  - question: 'Can I use this integration with private repositories?'
    answer: 'Yes, as long as your Personal Access Token has the `repo` scope, you can access and manage private repositories.'
  - question: 'What is the rate limit for GitHub API requests?'
    answer: 'Authenticated requests have a rate limit of 5,000 requests per hour. Unauthenticated requests are limited to 60 requests per hour.'
  - question: 'How do I create a cross-repository pull request?'
    answer: 'Use the format `username:branch-name` for the Head Branch field when creating a pull request from a fork or different repository.'
llmAnswer: 'The GitHub integration for Warpbase allows you to manage repositories, create issues and pull requests, add comments, and search repositories using GitHub REST API v3. Setup requires a Personal Access Token with appropriate scopes.'
---

The GitHub integration lets you manage your GitHub repositories, issues, and pull requests directly from Warpbase. We built this using GitHub's REST API v3, so you can automate your GitHub workflow without leaving your workspace.

Here's what you can do:

* Create and manage issues
* Create pull requests
* Search repositories
* Add comments to issues and PRs
* Get repository information

## Getting started

You'll need a GitHub Personal Access Token to use this integration. Here's how to set it up.

### Create your GitHub token

Head over to [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens) and click **"Generate new token"** → **"Generate new token (classic)"**.

Give it a name like "Warpbase Integration" and set an expiration (we recommend 90 days). For scopes, you'll need:

* **`repo`** - This gives you full control of private repositories. You'll need this for most operations like creating issues and PRs.
* **`read:org`** - Only if you're working with organization repositories
* **`read:user`** - For reading user profile data

Click **"Generate token"** and copy it immediately. GitHub won't show it to you again.

### Set your environment variable

Set the `GITHUB_TOKEN` environment variable with your token:

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

### Test it out

Try the "Get Repository" warp with a public repo to verify everything works:

* Owner: `octocat`
* Repository: `Hello-World`

If you see repository info with stars and forks, you're all set.

## What you can do

### Create issues

Use the `github/create-issue` warp to create a new issue in any repository.

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

### Get repository info

The `github/get-repository` warp gives you all the details about any repository.

Just provide the owner and repository name. You'll get back the name, description, stars, forks, language, and clone URLs.

```
Owner: facebook
Repository: react
```

### List issues

Use `github/list-issues` to list issues in a repo. You can filter by state (`open`, `closed`, or `all`), labels, assignee, and limit results (max 100, default 30).

You'll get an array of issues and the total count.

```
Owner: myusername
Repository: myproject
State: open
Labels: bug
Assignee: developer1
Limit: 50
```

### Get a specific issue

The `github/get-issue` warp pulls all the details for a single issue - title, body, state, labels, assignees, and author.

```
Owner: myusername
Repository: myproject
Issue Number: 42
```

### Create pull requests

The `github/create-pull-request` warp creates a new PR to merge changes between branches.

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

### Add comments

Use `github/add-comment` to add a comment to any issue or PR. The comment body supports Markdown.

You'll get back the comment ID and URL.

```
Owner: myusername
Repository: myproject
Issue Number: 42
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

### Search repositories

The `github/search-repositories` warp lets you search GitHub using their search syntax. You can sort by stars, forks, help-wanted-issues, or updated date, and limit results (max 100).

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

## Authentication

We use Personal Access Tokens (PATs) for authentication. It's the simplest way to connect to GitHub's API.

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

## How it works

All requests go to `https://api.github.com` with your token in the Authorization header. We use GitHub's REST API v3, so everything follows their standard format.

Rate limit info comes back in response headers - you'll see how many requests you have left and when the limit resets.

## Real-world examples

### Automated bug reporting

Create an issue automatically when your app detects a bug:

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

### Monitor repository stats

Check how your repo is doing:

```
Action: Get Repository
Owner: myusername
Repository: myproject
```

Then look at the stars, forks, and language stats.

### Issue triage

Filter issues to find what needs attention:

```
Action: List Issues
Owner: myusername
Repository: myproject
State: open
Labels: bug,needs-triage
Limit: 100
```

### Cross-repo pull requests

Create a PR from a fork using the `username:branch` format:

```
Action: Create Pull Request
Owner: upstream-org
Repository: upstream-repo
Title: Fix typo in README
Body: Fixed a typo in the installation instructions.
Head Branch: myusername:patch-1
Base Branch: main
```

### Find trending repos

Search for popular repositories:

```
Action: Search Repositories
Query: language:rust stars:>1000 created:>2024-01-01
Sort: stars
Order: desc
Limit: 20
```

## Troubleshooting

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

While not directly supported, you can combine GitHub webhooks with Warpbase to automatically create issues, update issues from external triggers, or sync data between systems.

## Resources

* [GitHub REST API Docs](https://docs.github.com/en/rest)
* [GitHub API Authentication](https://docs.github.com/en/rest/authentication)
* [Personal Access Tokens](https://github.com/settings/tokens)
* [GitHub Search Syntax](https://docs.github.com/en/search-github/searching-on-github)
* [GitHub API Rate Limits](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
* [GitHub Flavored Markdown](https://github.github.com/gfm/)

---

**Note**: This integration uses GitHub REST API v3. We're considering adding GraphQL API v4 support in the future.
