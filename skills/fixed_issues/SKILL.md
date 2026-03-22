---
name: fixed-issues
description: Reports on Production bugs and issues fixed and deployed to Production in the last week, with root cause, business impact, and fix details from Jira and Confluence. Provides Jira bug ticket number and link. USE FOR: weekly production bug fix reports; post-incident reviews; stakeholder updates on resolved defects.
---

# Fixed Production Issues Report

## Purpose

Generate a report of Jira bugs that were closed in the last seven days, enriched with root cause analysis, business impact, and fix details pulled from Jira and Confluence. The report gives stakeholders a concise view of what Production issues were resolved and how.

## Connectivity Check

**Before doing anything else**, verify the Atlassian MCP (Rovo) server is responding by making a lightweight Rovo tool call (such as listing available resources or running a minimal JQL query). If the server does not respond or returns an error, **stop immediately** and report:

> The Atlassian MCP Server (Rovo) is not responding. Cannot generate the fixed-issues report. Please check that the Rovo MCP server is running and configured correctly.

Do not attempt any further steps until connectivity is confirmed.

## Step 1 — Query Fixed Production Bugs

Use the Rovo MCP server to run the following JQL query and retrieve all matching issues:

```
issuetype = Bug
AND status changed to Closed during (-7d, now())
```

For each bug returned, collect:
- Issue key (e.g., `PROJ-456`)
- Issue summary / title
- Priority and severity (if available)
- Resolution date
- Assignee and/or team (if available)
- The Jira URL to the issue (construct as `https://<your-instance>.atlassian.net/browse/<issue-key>`)

If no bugs are returned, output:

> No Production bugs were fixed and closed in the last 7 days.

Then stop.

## Step 2 — Gather Supporting Context

For each bug found in Step 1, use the Rovo MCP server to gather supporting context:

1. **From Jira**: Fetch the bug's description, comments, root cause field, fix summary, labels, components, affected versions, and linked issues (e.g., parent epics or related incidents).
2. **From Confluence**: Search for pages linked to or mentioning the issue key. Look for incident reports, post-mortems, runbooks, or release notes that document the business impact, root cause, or fix.

Prioritise information that explains:
- What went wrong and who or what was affected (business impact)
- Why it happened (root cause), if documented
- What was done to fix it

## Step 3 — Generate the Report

Produce a Markdown report with the following structure for each fixed bug:

```
### <Issue Key>: <Issue Summary>

**Jira Link:** [<Issue Key>](<Jira URL>)
**Resolved:** <Resolution Date> | **Priority:** <Priority>

**Business Impact:**
<1–3 sentences describing what broke and the effect on users or the business.>

**Root Cause:**
<1–2 sentences on why the issue occurred. If not documented, write: *Root cause not documented.*>

**Fix:**
<1–2 sentences describing what was changed or deployed to resolve the issue.>
```

Separate each entry with a horizontal rule (`---`).

Prepend the report with a one-line header:

```
## Fixed Production Issues — Week of <start date> to <end date>
```

## Output Rules

- Keep each section to the stated sentence limits. Do not reproduce full Jira descriptions or Confluence pages verbatim.
- Always include a working Jira link for every bug.
- If a section's information cannot be found, use one of these fallbacks:
  - *Business impact not documented.*
  - *Root cause not documented.*
  - *Fix details not documented.*
- Do not include code-level implementation details unless essential to convey the fix to a business audience.
- List issues in order of priority (Critical → High → Medium → Low), then by resolution date (most recent first) within each priority group.
