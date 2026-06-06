---
name: completed-epics
description: Reports on Jira epics completed or released in the last week, with business context from Jira and Confluence. Provides epic number, description, Jira link, and a brief business summary.
  Use for weekly epic completion reports; sprint/release reviews; stakeholder updates on delivered work.
---

# Completed Epics Report

## Purpose

Generate a report of Jira epics that were completed or released in the last seven days, enriched with business context pulled from Jira and Confluence. The report gives stakeholders a concise view of what was delivered and why it matters.

## Connectivity Check

**Before doing anything else**, verify the Atlassian MCP (Rovo) server is responding by making a lightweight Rovo tool call (such as listing available resources or running a minimal JQL query). If the server does not respond or returns an error, **stop immediately** and report:

> The Atlassian MCP Server (Rovo) is not responding. Cannot generate the completed-epics report. Please check that the Rovo MCP server is running and configured correctly.

Do not attempt any further steps until connectivity is confirmed.

## Step 1 — Get the Atlassian Cloud Id

Use the Rovo MCP server to obtain the Atlassian Cloud ID for your Jira instance. This ID is required for subsequent API calls to fetch epics and related information. Also get the base URL for your Jira instance, which will be used to construct direct links to the epics. Prompt the user for the  and Atlassian base URL if they are not already configured, and get the Atlassian Cloud ID from the Rovo MCP server.


## Step 2 — Query Completed Epics

Use the Rovo MCP server to run the following JQL query and retrieve all matching epics:

```
issuetype = Epic
AND (status changed to Closed during (-7d, now()) OR status changed to Resolved during (-7d, now()))
```

For each epic returned, collect:
- Epic key (e.g., `PROJ-123`)
- Epic summary / title
- Status
- Resolution date
- Assignee and/or team (if available)
- The Jira URL to the epic (construct as `https://<your-instance>.atlassian.net/browse/<epic-key>`)

If no epics are returned, output:

> No epics were completed or released in the last 7 days.

Then stop.

## Step 3 — Gather Business Context

For each epic found in Step 1, use the Rovo MCP server to gather supporting context:

1. **From Jira**: Fetch the epic's description, acceptance criteria, labels, components, linked initiative or parent, and any relevant comments that describe business value or release notes.
2. **From Confluence**: Search for pages linked to or mentioning the epic key. Look for release notes, product briefs, or feature documentation that provides business context.

Prioritise information that explains *what problem was solved* and *what business value was delivered*, rather than implementation details.

## Step 4 — Generate the Report

Produce a Markdown report with the following structure for each completed epic:

```
### <Epic Key>: <Epic Summary>

**Jira Link:** [<Epic Key>](<Jira URL>)
**Completed:** <Resolution Date>

**Business Summary:**
<2–4 sentences describing what was delivered and the business value, drawn from Jira description and Confluence context.>
```

Separate each epic entry with a horizontal rule (`---`).

Prepend the report with a one-line header:

```
## Completed Epics — Week of <start date> to <end date>
```

## Output Rules

- Keep each business summary to 2–4 sentences. Do not reproduce full Jira descriptions or Confluence pages verbatim.
- Always include a working Jira link for every epic.
- If business context cannot be found for an epic, write: *No supporting documentation found in Jira or Confluence.*
- Do not include implementation or technical details unless they are essential to convey business impact.
- List epics in chronological order by resolution date (most recent first).
