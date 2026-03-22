# Devaide Agent Plugin

Research and delivery-tracking plugin for GitHub Copilot. Devaide combines GitHub and Atlassian MCP servers to help with repository investigation, pull request and issue research, Confluence documentation lookups, and Jira-based reporting for completed epics and fixed production issues.

## Installation

```bash
# Using Copilot CLI
copilot plugin install devaide@awesome-copilot
```

## What's Included

### Agents

- `devaide`: Copilot agent for GitHub delivery research, Confluence documentation lookups, and Jira work tracking across initiatives, epics, features, stories, and bugs.

### Skills

- `completed-epics`: Produces a weekly report of Jira epics completed or released in the last seven days, enriched with Jira and Confluence business context.
- `fixed-issues`: Produces a weekly report of production bugs closed in the last seven days, including business impact, root cause, and fix summary from Jira and Confluence.

## MCP Servers

The MCP configuration lives in [.mcp.json](.mcp.json) and defines these backends:

- `github`: GitHub MCP endpoint for repository, issue, pull request, branch, release, and search operations.
- `rovo`: Atlassian Rovo MCP endpoint for Jira and Confluence operations.

Atlassian access requires the `atlassian_auth` prompt input configured in [.mcp.json](.mcp.json).

## Repository Layout

- [agents/devaide.md](agents/devaide.md): main agent definition and operating instructions.
- [skills/completed_epics/SKILL.md](skills/completed_epics/SKILL.md): weekly completed epics reporting workflow.
- [skills/fixed_issues/SKILL.md](skills/fixed_issues/SKILL.md): weekly fixed production issues reporting workflow.

## Source

This repository is a custom GitHub Copilot plugin focused on agent behavior and operational guidance rather than application code.
