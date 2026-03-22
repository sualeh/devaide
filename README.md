# Devaide

## What is the Devaide Agent Plugin

This repository contains a custom GitHub Copilot agent plugin called Devaide.

The plugin helps with engineering research and delivery tracking by using MCP servers to:

- Inspect GitHub repositories, pull requests, issues, branches, releases, and search results.
- Search Atlassian documentation in Confluence.
- Find completed and pending Jira work items across initiatives, epics, features, stories, and bugs.

## Where The Agent Is Defined

The agent definition is in [agents/devaide.md](agents/devaide.md).

## MCP Servers Used

The MCP configuration is in [.mcp.json](.mcp.json) and defines:

- github: GitHub MCP endpoint for repository and code-delivery operations.
- rovo: Atlassian Rovo MCP endpoint for Jira and Confluence operations.

## Notes

- Atlassian access requires the `atlassian_auth input` configured in [.mcp.json](.mcp.json).
- This repo is focused on agent behavior and operational guidance rather than application code.
