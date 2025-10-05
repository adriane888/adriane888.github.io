---
layout: post
title: "Copilot Spaces"
date: 2025-10-05 00:00:00 +0000
categories: copilot github ai
---

## What Is Copilot Spaces?
**Copilot Spaces** is the newest iteration of collaborative AI tooling from GitHub. It became generally available on **September 24th**. I’ll admit—there’s been a whirlwind of new and replacement tools lately—but this one’s a welcome addition.

I first noticed it while working with Copilot Knowledge Bases. I was notified that Knowledge Bases were being retired and replaced by Spaces. Knowledge Bases often felt clunky and tedious to stand up. Spaces are more straightforward and provide better utility (IMO).

## Getting Started
Let’s kick things off with the setup, then we’ll go deeper.

1. Go to: <https://github.com/copilot/spaces> (or click the Copilot icon in the top-right of GitHub, then choose Spaces in the left panel).
2. Click **Create space** and give it a meaningful name.
3. Choose the owner (your user or an organization if you plan to share it broadly).
4. Click **Create space**.
5. (Optional but recommended) Add a description. (It doesn’t affect responses directly, but it helps people understand intent.)

## Adding Context (The Real Power)
In AI, **context is king**. Spaces let you layer different types of context sources:

**Instructions**  
Define Copilot’s role (up to 4,000 characters). Align the description of the space with its instructions—especially if you plan to share it. Be concise and purposeful.

**Files & Repos**  
Spaces pull the latest code from the repository’s default branch (usually `main`). For best results, include only the most relevant folders/files instead of the entire tree.

**Linked Files, Pull Requests, and Issues**  
Currently limited to GitHub content. Paste URLs for PRs and issues. (Wishlist: future support for Confluence/Jira links.)

**Upload File / Add Text Content**  
Straightforward: add images, text files, documents, spreadsheets, or direct text blocks to enrich context.

## Ways to Use a Space
You have two primary interaction modes:

1. **In the GitHub Spaces UI** – Open the space and start chatting.
2. **In Your IDE** – The more powerful option: combine file context + Space context.

### When It Shines
**1. Onboarding / Poor Documentation**  
Curate Markdown guides, examples, architectural notes, and process docs into a Space so new or junior devs can self-serve—plus accelerate creation of missing docs.

**2. Distributed / Multi-Repo Systems**  
Modern systems are often spread across many repos. Keeping mental context straight is hard. A Space that unifies shared references across those repos saves time. Create one per subsystem or domain.

## Using Spaces in Your IDE
Your IDE needs two components:

- GitHub Copilot extension
- GitHub MCP Server (for Spaces integration)

Links:
- MCP Server: <https://github.com/mcp/github/github-mcp-server>
- Copilot VS Code Extension: install from the VS Code Extensions panel

In the chat box (once configured):

1. Run: `list_copilot_spaces` – lists available Spaces
2. Then: `get_copilot_space <space-name>` – attaches that Space’s context to your prompt

## Workflow Boost
Used thoughtfully, Spaces can accelerate:
- Consistent architectural decisions
- Faster ramp for new engineers
- Cross-repo investigations
- Automation pattern reuse

## Final Thoughts
It’s not a perfect tool, but used well it can help you and your team **achieve goals faster**—and maybe even make the process a little more fun.

If you’ve tried Spaces already, what use case helped you most? 
