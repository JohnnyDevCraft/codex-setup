# Azure DevOps MCP

## Name

Azure DevOps MCP

## Category

MCP Tool

## URL

- GitHub repo: https://github.com/microsoft/azure-devops-mcp
- Package: https://www.npmjs.com/package/@azure-devops/mcp

## Tool Description

Azure DevOps MCP is Microsoft’s Model Context Protocol (MCP) server for Azure DevOps (ADO). It exposes ADO capabilities (Work Items, Repos/PRs, Pipelines, Wiki, Search, etc.) to MCP-compatible clients so an agent can retrieve and act on ADO data through tool calls.

For our usage, the primary value is:

- Retrieve Work Items (single, batch, query, revisions, and comments)
- Retrieve PR comment threads and comments

## Primary Use Cases

- Read a work item by ID and summarize status/fields/links
- Search for work items, then hydrate the matching IDs
- List and read work item comments to capture context and decisions
- Retrieve a PR by ID and list its discussion threads/comments for review
- Pull PR change metadata (and then use comments/threads to discuss review feedback)

## Dependencies

- Azure DevOps organization access (permissions to read Work Items and Repos/PRs)
- Node.js 20+
- An MCP-capable client (VS Code + Copilot Agent Mode, Cursor, Claude Desktop, etc.)
- Authentication:
  - Interactive Microsoft login (default), or
  - Azure DevOps Personal Access Token (PAT) via environment variable (recommended for automation)

## Install Instructions

### Install via NPX (recommended)

Most clients support running MCP servers over stdio. For VS Code, add `.vscode/mcp.json` with an Azure DevOps organization prompt and run the server via `npx`:

```json
{
  "inputs": [
    {
      "id": "ado_org",
      "type": "promptString",
      "description": "Azure DevOps organization name (e.g. 'contoso')"
    }
  ],
  "servers": {
    "ado": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "${input:ado_org}"]
    }
  }
}
```

Notes:

- The first time an ADO tool is executed, the default auth flow may open a browser to sign in.
- Ensure the signed-in identity has access to the target organization/projects.

### Token (PAT) auth via environment variable

For non-interactive/automated scenarios, set a PAT in an environment variable and pass the server `--authentication envvar`.

1) Set the environment variable:

```bash
export ADO_MCP_AUTH_TOKEN="your-azure-devops-pat"
```

2) Update `mcp.json`:

```json
{
  "inputs": [
    {
      "id": "ado_org",
      "type": "promptString",
      "description": "Azure DevOps organization name (e.g. 'contoso')"
    }
  ],
  "servers": {
    "ado": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "${input:ado_org}", "--authentication", "envvar"]
    }
  }
}
```

Security notes:

- Never commit PATs.
- Prefer storing PATs in the client’s secrets manager or your shell’s secure environment tooling.

### Limit tool surface area with Domains (recommended)

Azure DevOps has a large surface area. Use Domains to load only the tool groups you need.

For Work Items + PR comments, a good default is:

- `core` (recommended baseline)
- `work` and `work-items` (Work Items)
- `repositories` (Repos/PRs/threads/comments)

Example `mcp.json` server args with domains:

```json
{
  "inputs": [
    {
      "id": "ado_org",
      "type": "promptString",
      "description": "Azure DevOps organization name (e.g. 'contoso')"
    }
  ],
  "servers": {
    "ado_filtered": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "${input:ado_org}", "-d", "core", "work", "work-items", "repositories"]
    }
  }
}
```

## Tool Commands

Not applicable (MCP server is executed by the MCP client).

When troubleshooting locally, it is often helpful to confirm Node can run the package:

```bash
node -v
npx -y @azure-devops/mcp --help
```

## MCP JSON

See `Install Instructions` for working `.vscode/mcp.json` examples.

## Tool Inputs

These are the most common inputs we expect an agent to need when using this MCP:

### Organization

- Purpose: Target ADO organization
- Format: Organization name (e.g. `contoso`) as provided to the MCP server at startup

### Project

- Purpose: Scope repo/work-item queries
- Format: ADO project name (string) or project ID (UUID), depending on tool

### Work Item ID(s)

- Purpose: Retrieve or update specific work items
- Format: Integer ID or list of integer IDs

### Repo and PR

- Purpose: Retrieve PR details and comment threads
- Format:
  - Repo name or repo ID (UUID)
  - PR ID (integer)

## Outputs

Azure DevOps MCP tools typically return JSON objects that mirror Azure DevOps REST API responses.

For our main scenarios:

- Work item retrieval returns fields, relations (links), and metadata for the item(s).
- Work item comments returns a list of comments with authors, timestamps, and content.
- PR threads/comments returns discussion threads, each with one or more comments, plus thread metadata (status, properties, and (when present) file/line context).

## AI Usage Notes

- Prefer narrow Domains to reduce noise and avoid client tool limits.
- When retrieving a work item, ask the MCP for the work item first, then follow up with comments and revision history if needed.
- For PR review context, retrieve PR metadata and then list threads/comments before summarizing “what needs action”.

### Common tool calls for our workflows

Work Items:

- `mcp_ado_wit_get_work_item` (single work item)
- `mcp_ado_wit_get_work_items_batch_by_ids` (batch hydrate by IDs)
- `mcp_ado_wit_query_by_wiql` (query via WIQL)
- `mcp_ado_wit_list_work_item_comments` (work item comments)
- `mcp_ado_wit_list_work_item_revisions` (audit trail)

PR Comments:

- `mcp_ado_repo_get_pull_request_by_id` (PR metadata)
- `mcp_ado_repo_list_pull_request_threads` (comment threads)
- `mcp_ado_repo_list_pull_request_thread_comments` (comments in a thread)

## Constraints and Limits

- Requires ADO permissions for the org/project/repo/work items being accessed.
- Interactive auth may require a browser login the first time a tool is used.
- Tool surface area is large; using Domains is strongly recommended.

## Authentication or Access Requirements

- Default: interactive Microsoft account sign-in when the first tool is executed.
- Automation: PAT via `ADO_MCP_AUTH_TOKEN` and `--authentication envvar`.

## Output or Deliverables

- Retrieved work item data for summarization and decision support
- Work item comment history for context and requirements
- PR discussion threads and comments for code-review feedback triage

## Example Requests

- “Get work item 12345 and summarize its current state, acceptance criteria, and links.”
- “List comments on work item 12345 and highlight any decisions or blockers.”
- “Run a WIQL query to find active bugs assigned to me in project X, then summarize the top 10 by priority.”
- “For PR 678 in repo Y, list all comment threads and summarize requested changes.”
- “In PR 678, show unresolved threads (or threads that look like action items) and group them by area.”

