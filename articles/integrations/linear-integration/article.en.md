---
title: 'Linear Integration Guide for JoAi'
description: 'Set up Linear integration with JoAi in 5 minutes. Create issues, manage teams, update states, and automate project workflows using Linear GraphQL API. Complete setup guide.'
category: 'integrations'
tags: ['linear', 'integration', 'api', 'project-management', 'graphql']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
draft: true
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['linear integration', 'linear integration setup', 'connect linear joai', 'linear api integration', 'linear project management', 'linear workflow automation', 'linear graphql api', 'linear api key', 'linear issues api', 'linear teams']
relatedArticles: []
faqs:
  - question: 'How long does Linear integration setup take?'
    answer: 'Setup takes approximately 5 minutes. You need to create a Linear API key and set it as an environment variable.'
  - question: 'What permissions does the Linear integration need?'
    answer: 'The integration requires a Linear API key. Your API key inherits the permissions of your Linear user account - you can access teams you are a member of and issues you have permission to view.'
  - question: 'Can I use this integration with all Linear teams?'
    answer: 'Yes, you can access all teams you are a member of. If you are an admin, you can manage all teams and issues in your workspace.'
  - question: 'What is the rate limit for Linear API requests?'
    answer: 'Authenticated requests have a rate limit of 10,000 requests per hour. The integration handles rate limiting automatically.'
  - question: 'How do I find team IDs and issue IDs?'
    answer: 'Use the "List Teams" warp to find team IDs and "List Issues" to find issue IDs. The response includes both IDs and human-readable identifiers.'
llmAnswer: 'Set up Linear integration in JoAi by creating an API key from Linear Settings > API and setting it as the LINEAR_API_KEY environment variable. This enables creating issues, managing teams, updating states, and adding comments via Linear GraphQL API.'
---

The Linear integration for JoAi lets you manage your Linear issues, teams, and projects directly from your workspace. This Linear integration uses Linear's GraphQL API, so you can automate your project management workflow without leaving JoAi. Setting up the Linear integration takes just 5 minutes and unlocks powerful automation capabilities.

## What You'll Learn

* How to set up Linear integration with API keys
* Creating and managing Linear issues and teams
* Updating issue states and priorities
* Adding comments to track progress
* Troubleshooting common Linear integration errors
* Best practices for Linear API authentication and security

## How to Set Up Linear Integration

You'll need a Linear API key to use this Linear integration. Here's how to set it up in just a few minutes.

### Create Your Linear API Key

Log in to your Linear account at [linear.app](https://linear.app) and navigate to **Settings** → **API** (or go directly to [https://linear.app/settings/api](https://linear.app/settings/api)).

Click **"Create API Key"** and give it a name like "JoAi Integration".

**Important**: Copy the API key immediately - Linear won't show it to you again!

### Configure Linear Integration Environment Variable

Set the `LINEAR_API_KEY` environment variable with your **Linear API key**:

**macOS/Linux:**
```bash
export LINEAR_API_KEY="your_api_key_here"
```

To make it stick, add it to your `~/.zshrc` or `~/.bashrc`:
```bash
echo 'export LINEAR_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

**Windows (PowerShell):**
```powershell
$env:LINEAR_API_KEY="your_api_key_here"
```

**Windows (Command Prompt):**
```cmd
setx LINEAR_API_KEY "your_api_key_here"
```

**Docker:**
```bash
docker run -e LINEAR_API_KEY="your_api_key_here" ...
```

### Verify Linear Integration Setup

Try the "List Teams" warp to verify your **Linear integration** works. If successful, you'll receive a list of all teams in your Linear workspace.

## Linear Integration Features and Actions

### List Linear Teams

Use the `linear/list-teams` warp to retrieve all teams in your Linear workspace. This is usually the first step to find team IDs needed for other operations.

You'll get back:
* `TEAMS`: Array of team objects with ID, name, key, and description
* `COUNT`: Number of teams found

Use this to find team IDs before creating or listing issues.

### Create Linear Issues

Use the `linear/create-issue` warp to create a new **Linear issue** in any team through the Linear integration.

You'll need:
* Team ID (required) - Get this from "List Teams"
* Title (required)
* Description (optional, supports Markdown)
* Assignee ID (optional)
* Priority (optional): `0` = No priority, `1` = Urgent, `2` = High, `3` = Medium, `4` = Low

You'll get back the issue ID, title, URL, identifier (e.g., "ENG-123"), and success status.

Here's an example:
```
Team ID: abc123def456
Title: Fix login bug
Description: The login form is not validating email addresses correctly.
Priority: 2
```

### List Linear Issues

Use `linear/list-issues` to list **Linear issues** in a team through the integration. You can filter by assignee, state, and limit results (max 50, default 20).

You'll get an array of issues with ID, identifier, title, description, state, assignee, priority, and creation date.

```
Team ID: abc123def456
State: started
Limit: 50
```

### Get Specific Linear Issue Details

The `linear/get-issue` warp pulls all the details for a single **Linear issue** - ID, identifier, title, description, state, assignee, priority, URL, and creation date.

```
Issue ID: xyz789ghi012
```

### Update Linear Issues

The `linear/update-issue` warp lets you update an existing **Linear issue** through the integration. You can change title, description, state, assignee, or priority.

You'll need the issue ID and any fields you want to update (leave fields empty to keep current values).

You'll get back the updated issue details and success status.

```
Issue ID: xyz789ghi012
State ID: started
Priority: 1
```

### Add Comments to Linear Issues

Use `linear/add-comment` to add a comment to any **Linear issue** through the integration. The comment body supports Markdown.

You'll get back the comment ID, body, author, creation date, and success status.

```
Issue ID: xyz789ghi012
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

## Linear Integration Authentication

We use API key authentication for Linear integration. Your API key provides full access to your Linear workspace based on your user permissions.

### What Permissions You Need

Your API key inherits the permissions of your Linear user account:
* **Full access**: If you're an admin, you can manage all teams and issues
* **Team access**: You can only access teams you're a member of
* **Issue access**: You can only access issues you have permission to view

### Security Tips

A few things to keep in mind:

* Rotate API keys regularly
* Use API keys only from secure environments
* Never commit API keys to version control
* Use environment variables or secret managers in production
* Revoke keys immediately if compromised

### Rate Limits

Linear limits authenticated requests to 10,000 per hour. You'll see rate limit info in response headers. The Linear integration handles rate limiting automatically.

## How Linear Integration Works

All Linear integration requests go to `https://api.linear.app/graphql` with your API key in the Authorization header. We use Linear's GraphQL API, so everything follows their standard format.

GraphQL responses include data and any errors. This Linear integration handles all the API communication for you.

## Linear Integration Use Cases and Examples

### Automated Bug Reporting

Create a **Linear issue** automatically when your app detects a bug using the Linear integration:

```
Action: Create Issue
Team ID: [Your Team ID]
Title: [BUG] Login validation failing
Description: ## Description
The login form is not validating email addresses correctly.

## Steps to Reproduce
1. Go to login page
2. Enter invalid email
3. Submit form

Priority: 2 (High)
```

### Linear Issue Triage Workflow

Filter **Linear issues** to find what needs attention using the Linear integration:

```
Step 1: List Issues
Team ID: abc123def456
State: unstarted

Step 2: Get Issue
Issue ID: [from list above]

Step 3: Update Issue
Issue ID: [from step 2]
State ID: started
Assignee ID: [your user ID]
```

### Daily Standup Automation

List all started issues for a team:

```
Action: List Issues
Team ID: abc123def456
State: started
Limit: 50
```

### Issue State Management

Move an issue through workflow states:

```
Action: Update Issue
Issue ID: xyz789ghi012
State ID: started

# Later, when work is done:
Action: Update Issue
Issue ID: xyz789ghi012
State ID: completed
```

### Progress Tracking with Comments

Add comments to track progress:

```
Action: Add Comment
Issue ID: xyz789ghi012
Comment Body: ## Progress Update

- [x] Implemented login validation
- [x] Added error messages
- [ ] Write tests
- [ ] Code review

ETA: Tomorrow
```

## Finding IDs

### Team IDs

Use the **List Teams** warp to find team IDs. The response includes:
* `id`: Use this for team operations
* `name`: Team name for reference
* `key`: Team key (short identifier)

### Issue IDs

Use the **List Issues** warp to find issue IDs. The response includes:
* `id`: Use this for issue operations
* `identifier`: Human-readable identifier (e.g., "ENG-123")

### User/Assignee IDs

To find user IDs for assignment:
1. Use **Get Issue** on an existing issue
2. Check the `assignee.id` field in the response
3. Or check Linear's web interface user URLs

### State IDs

Linear states are typically:
* `backlog`: Issues in backlog
* `unstarted`: Not started yet
* `started`: In progress
* `completed`: Done
* `canceled`: Cancelled

Use **Get Issue** to see the current state ID, or check Linear's API documentation for state IDs in your workspace.

## Troubleshooting Linear Integration Issues

### "Unauthorized" Error

Your API key isn't working. Check that:
* The `LINEAR_API_KEY` environment variable is set correctly
* The API key hasn't been revoked
* The API key is valid and not expired

If all else fails, regenerate the API key.

### "Team not found" Error

Linear can't find the team. Make sure:
* The team ID is correct (use "List Teams" to verify)
* You're a member of the team
* You're using the team ID (not the team key)

### "Issue not found" Error

Linear can't find the issue. Check that:
* The issue ID is correct (use "List Issues" to verify)
* You have permission to view the issue
* You're using the issue ID (not the identifier like "ENG-123")

### "Invalid state" Error

The state ID is invalid. Verify that:
* You're using a valid state ID from your workspace
* The state exists in your Linear workflow
* Use "Get Issue" to see valid state IDs

### Rate Limit Exceeded

You're hitting Linear's rate limits. Wait for the reset or implement throttling in your app. Authenticated requests get 10,000 requests/hour, which should be plenty for most use cases.

### Quick Debugging Tips

* Start with "List Teams" to verify your setup works
* Use List operations to find correct IDs
* Verify you have access to teams/issues
* Read the error messages - they usually tell you exactly what's wrong

## Best Practices

### ID Management

Always use "List Teams" first to get team IDs. Store team IDs for reuse. Use issue identifiers (like "ENG-123") for human reference, but use IDs for API calls.

### State Management

Understand your workspace's workflow states. Use consistent state transitions. Document state changes in comments.

### Error Handling

Always check for GraphQL errors in responses. Implement retry logic for rate limit errors, and log everything for debugging. Your users will thank you for clear error messages.

### Rate Limiting

Keep an eye on rate limit headers. Use exponential backoff for retries, cache responses when you can, and batch operations when possible.

### Security

Never commit API keys to version control. Use `.gitignore` for environment files, rotate API keys regularly, and audit key usage regularly.

### Issue Management

Use descriptive titles. Include detailed descriptions with Markdown. Set appropriate priorities. Assign issues promptly. Add comments for progress updates.

## Advanced Usage

### GraphQL Variables

All warps use GraphQL variables for safe parameter injection. Variables are automatically escaped and typed correctly.

### Markdown Support

Linear supports GitHub Flavored Markdown in issue descriptions, comments, and all text fields. You can use headers, lists, code blocks, task lists, tables, mentions (@username), and issue references (#123).

### Workflow Automation

Combine multiple warps for automation:
1. **List Issues** → Find issues needing attention
2. **Get Issue** → Get details
3. **Update Issue** → Change state/assignee
4. **Add Comment** → Log the change

### Integration Patterns

* **CI/CD Integration**: Create issues from build failures
* **Monitoring Integration**: Create issues from alerts
* **Support Integration**: Create issues from support tickets
* **Code Review**: Update issues when PRs are merged

## Resources

* [Linear API Documentation](https://developers.linear.app/docs/graphql/overview)
* [Linear GraphQL API Reference](https://developers.linear.app/docs/graphql/working-with-the-graphql-api)
* [Linear API Authentication](https://developers.linear.app/docs/graphql/authentication)
* [Linear GraphQL Explorer](https://linear.app/developers/graphql)
* [Linear API Rate Limits](https://developers.linear.app/docs/graphql/working-with-the-graphql-api#rate-limits)
* [Linear Markdown Guide](https://linear.app/docs/markdown)

---

## Conclusion

You're now ready to use the Linear integration in JoAi! This Linear integration enables you to automate your project management workflow, manage issues and teams, and streamline your development process. Start with simple operations like creating issues, then explore more advanced features like automated state management and progress tracking.

Remember to keep your API key secure, rotate it regularly, and monitor your API rate limits. For more advanced automation, consider combining this Linear integration with webhooks and other JoAi features. Explore other JoAi integrations to build comprehensive automation workflows.

**Note**: This Linear integration uses Linear's GraphQL API. For the latest features and capabilities, refer to [Linear's API documentation](https://developers.linear.app/docs/graphql/overview).
