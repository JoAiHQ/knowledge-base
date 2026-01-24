---
title: "Teach Your AI to Build Warps with Skills"
description: "Learn how to use Warp Protocol Skills to give AI coding assistants the knowledge they need to create blockchain-enabled Warps automatically."
category: "guides"
tags: ["warps", "ai skills", "blockchain", "developer tools", "automation"]
author: "JoAi Team"
publishedAt: "2026-01-24"
updatedAt: "2026-01-24"
featured: true
draft: true
difficulty: "intermediate"
readTime: 6
keywords: ["warp protocol skills", "ai coding assistant", "warp creation", "blockchain automation", "npx skills add"]
relatedArticles: ["what-is-an-ai-agent", "what-is-model-context-protocol"]
faqs:
  - question: "What AI coding assistants support Warp Skills?"
    answer: "Any AI assistant that supports the skills protocol, including Cursor, Windsurf, Cline, Zed, Roo Code, and Gemini CLI."
  - question: "Do I need blockchain experience to use Warp Skills?"
    answer: "No. The skills teach your AI assistant the complete Warp specification, so you can describe what you want in plain language."
  - question: "Can I create custom skills for my own protocols?"
    answer: "Yes. Skills are just markdown files with structured documentation. You can fork the JoAi skills repo and add your own."
llmAnswer: "Warp Protocol Skills are structured documentation files that teach AI coding assistants how to create Warps—blockchain-enabled actions that AI agents can execute across 11+ chains."
---

# Teach Your AI to Build Warps with Skills

What if your AI coding assistant could create blockchain transactions, token transfers, and smart contract calls—just from a plain-language description?

That's exactly what **Warp Protocol Skills** enable.

## What Are Warp Skills?

Skills are structured documentation files that give AI coding assistants specialized knowledge. Think of them as training materials that your AI reads before helping you code.

Warp Protocol Skills teach your AI:
- The complete Warp v3 specification
- All 7 action types (transfer, contract, query, collect, link, mcp, prompt)
- Multi-chain support across 11 blockchains
- Advanced features like i18n, alerts, and output mapping

## Why Use Skills Instead of Documentation?

You could paste documentation into your AI chat. But skills are different:

| Pasting Docs | Using Skills |
|--------------|--------------|
| Manual copy/paste each time | Install once, use forever |
| Overwhelming context dumps | Structured, AI-optimized format |
| Gets outdated fast | Update with a single command |
| No validation guidance | Includes rules and best practices |

Skills integrate directly with your IDE. Your AI loads them automatically when relevant.

## Installation

One command adds Warp skills to any supported project:

```bash
npx skills add JoAiHQ/skills
```

This installs the latest Warp Protocol skills into your project's `.skills/` directory.

**Supported AI assistants:**
- Cursor
- Windsurf
- Cline
- Zed
- Roo Code
- Gemini CLI

## What You Can Build

Once installed, just describe what you want. Your AI handles the Warp specification:

### Token Transfers

> "Create a Warp that lets users send ETH on Base chain with a custom amount"

Your AI generates a complete transfer Warp with dynamic inputs, chain configuration, and proper validation.

### Smart Contract Calls

> "Build a Warp to mint an NFT on Polygon, collecting the user's name as metadata"

The AI creates a contract action with ABI encoding, input collection, and transaction parameters.

### Multi-Step Workflows

> "Chain together a token swap followed by a confirmation message"

Skills include chaining documentation, so your AI knows how to link Warps together.

### AI Agent Actions

> "Create an MCP action that queries a price oracle before executing a trade"

The new v3 `mcp` and `prompt` actions enable AI-to-blockchain workflows.

## What's Included

The skills package covers the complete Warp v3 specification:

**Action Types:**
- `transfer` – Move tokens across chains
- `contract` – Call smart contracts
- `query` – Read blockchain state
- `collect` – Gather user inputs
- `link` – Navigate to URLs
- `mcp` – Model Context Protocol integration
- `prompt` – AI text generation

**Supported Chains:**
MultiversX, Sui, Ethereum, Base, Arbitrum, Polygon, Somnia, Solana, NEAR, Vibechain, Fastset

**Advanced Features:**
- Internationalization (i18n) for multi-language Warps
- Alerts system for execution notifications
- Output mapping for result transformations
- Variable interpolation with static and dynamic sources

## Example: Creating a Donation Warp

Here's a real interaction with an AI assistant using Warp skills:

**You:** "Create a Warp for accepting ETH donations on Base with a thank you message"

**AI generates:**

```json
{
  "protocol": "warp:0.3.0",
  "name": "Support Our Project",
  "title": "Make a Donation",
  "description": "Support our work with an ETH donation",
  "actions": [
    {
      "type": "transfer",
      "chain": "base",
      "label": "Donate ETH",
      "destination": {
        "address": "0x..."
      },
      "inputs": [
        {
          "name": "amount",
          "type": "amount-native",
          "source": "user",
          "required": true
        }
      ]
    }
  ],
  "messages": {
    "success": "Thank you for your support! 🙏"
  }
}
```

No blockchain knowledge required. The AI knows the spec.

## Keeping Skills Updated

Skills evolve with the protocol. Update anytime:

```bash
npx skills update
```

This pulls the latest documentation, including new chains, action types, and features.

## The Bottom Line

Warp Protocol Skills turn any AI coding assistant into a blockchain development partner. You describe the outcome. The AI handles the specification.

Stop memorizing protocol specs. Let your AI do the heavy lifting.

**Get started:**

```bash
npx skills add JoAiHQ/skills
```

Then just ask your AI to create a Warp.
