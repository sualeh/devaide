# Devaide Agent Plugin

Research and delivery-tracking plugin for GitHub Copilot. Devaide combines GitHub and Atlassian MCP servers to help with repository investigation, pull request and issue research, Confluence documentation lookups, and Jira-based reporting for completed epics and fixed production issues.

## What's Included

### Agent

- `devaide`: Copilot agent for GitHub delivery research, Confluence documentation lookups, and Jira work tracking across initiatives, epics, features, stories, and bugs.

### Skills

- `completed-epics`: Produces a weekly report of Jira epics completed or released in the last seven days, enriched with Jira and Confluence business context.
- `fixed-issues`: Produces a weekly report of production bugs closed in the last seven days, including business impact, root cause, and fix summary from Jira and Confluence.

### MCP Servers

Defined in [.mcp.json](.mcp.json) and registered automatically when the plugin is enabled:

- `devaide-github`: GitHub MCP endpoint for repository, issue, pull request, branch, release, and search operations.
- `devaide-rovo`: Atlassian Rovo MCP endpoint for Jira and Confluence operations.

## Installing devaide in Another Project

### Option 1 — GitHub Copilot CLI (recommended)

Install from the [awesome-copilot](https://github.com/github/awesome-copilot) marketplace:

```bash
copilot plugin install devaide@awesome-copilot
```

VS Code automatically discovers plugins installed by the Copilot CLI from `~/.copilot/installed-plugins/`. After installing, restart VS Code and the plugin appears in **Agent Plugins - Installed** in the Extensions view.

To install directly from this repository instead of the marketplace:

```bash
copilot plugin install sualeh/devaide
```

### Option 2 — VS Code local plugin (manual clone)

1. Clone this repository to a local path:

   ```bash
   git clone https://github.com/sualeh/devaide /path/to/devaide
   ```

2. Register the path in VS Code settings (user or workspace `.vscode/settings.json`):

   ```json
   "chat.pluginLocations": {
     "/path/to/devaide": true
   }
   ```

3. Restart VS Code. The plugin appears in **Agent Plugins - Installed**.

### Option 3 — VS Code marketplace

1. Open the Extensions view (`Ctrl+Shift+X` / `⇧⌘X`).
2. Search for `@agentPlugins`.
3. Find **devaide** and click **Install**.

> **Note:** Agent plugins must be enabled in your organization. If the `@agentPlugins` search returns nothing, ask your administrator to enable `chat.plugins.enabled`.

### Option 4 — Workspace plugin recommendation

To recommend devaide to your whole team, add the following to `.github/copilot/settings.json` in your repository:

```json
{
  "enabledPlugins": {
    "devaide@awesome-copilot": true
  }
}
```

Team members see an install prompt the first time they open chat in that workspace.

## Required Configuration — Atlassian Auth

The `devaide-rovo` MCP server requires an Atlassian API token. On first use, VS Code prompts for the `atlassian_auth` secret.

**How to generate the token:**

1. Go to [https://id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens) and create an API token.
2. Encode your credentials as Base64:

   ```bash
   echo -n "your-email@example.com:your-api-token" | base64
   ```

3. Enter the resulting Base64 string when VS Code prompts for `atlassian_auth`.

The GitHub MCP server (`devaide-github`) uses your existing GitHub Copilot authentication — no additional setup is needed.

## Using the Plugin

### Invoke the agent

In GitHub Copilot Chat, type `@devaide` to route your message to the devaide agent:

```
@devaide What pull requests were merged to main this week?
@devaide Find the Confluence page for our authentication architecture.
@devaide Show open Jira stories in the Payments epic.
```

### Run a skill

Attach a skill with `#` in chat:

```
#completed-epics
#fixed-issues
```

Skills can also be enabled via **Configure Skills** in the Chat view header.

## Repository Layout

- [plugin.json](plugin.json): plugin manifest (name, version, agents, skills, MCP servers).
- [.mcp.json](.mcp.json): MCP server definitions for GitHub and Atlassian Rovo.
- [agents/devaide.md](agents/devaide.md): main agent definition and operating instructions.
- [skills/completed_epics/SKILL.md](skills/completed_epics/SKILL.md): weekly completed epics reporting workflow.
- [skills/fixed_issues/SKILL.md](skills/fixed_issues/SKILL.md): weekly fixed production issues reporting workflow.
