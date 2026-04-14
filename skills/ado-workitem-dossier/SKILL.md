---
name: ado-workitem-dossier
description: Export an Azure DevOps work item (+ parent + children) into a single Markdown dossier file in `WorkItems/<id>-<title>.md`.
---

# ADO Work Item Dossier (Markdown Export)

Use this skill when the user provides an Azure DevOps Work Item ID and wants a single Markdown file containing key details for:

- The provided Work Item
- Its Parent Work Item (if any)
- Any Child Work Items (if any)

The output is saved in the current repo under `WorkItems/` as:

`<WorkItemId>-<Title>.md`

## Inputs required

- `workItemId` (integer)

Optional (ask only if needed):

- `project` (ADO project name) if tool calls require it in this environment

## Data to retrieve (for each item: target, parent, children)

Collect the following, when present:

- Description
- Acceptance Criteria
- Repro Steps (“Repo Steps”)
- System Info
- Discussion Threads (Comments)
- Effort
- CreatedBy
- AssignedTo

## Field mapping (best-effort)

ADO processes vary; use these field reference names when available, and fall back gracefully:

- Title: `System.Title`
- Type: `System.WorkItemType`
- State: `System.State`
- Description: `System.Description`
- Acceptance Criteria: `Microsoft.VSTS.Common.AcceptanceCriteria` (common for User Story)
- Repro Steps (“Repo Steps”): `Microsoft.VSTS.TCM.ReproSteps` (common for Bug)
- System Info: `Microsoft.VSTS.TCM.SystemInfo` (common for Bug)
- Effort: prefer `Microsoft.VSTS.Scheduling.Effort`, else `Microsoft.VSTS.Scheduling.StoryPoints`
- CreatedBy: `System.CreatedBy`
- AssignedTo: `System.AssignedTo`

If a requested label does not exist, include it as `N/A` (do not hallucinate content).

## Relationship discovery

1) Fetch the target work item with relations:
   - Call `mcp__ado__wit_get_work_item` with `expand=all` to get `relations`.
2) Determine Parent ID (if any):
   - Look for a relation where `rel` is `System.LinkTypes.Hierarchy-Reverse` and parse the work item ID from the `url`.
3) Determine Child IDs (if any):
   - Look for relations where `rel` is `System.LinkTypes.Hierarchy-Forward` and parse IDs from each `url`.

Then fetch parent and children with `mcp__ado__wit_get_work_item` and their comments with `mcp__ado__wit_list_work_item_comments`.

## Comments / “Discussion Threads”

- Use `mcp__ado__wit_list_work_item_comments` for each item.
- Render in Markdown as a chronological list with:
  - author display name
  - created date/time
  - (edited?) indicator if present
  - comment text (convert HTML-to-Markdown when needed; render inline, not in a code block)

## HTML → Markdown conversion (required)

For these fields (and for comment bodies), Azure DevOps frequently returns HTML:

- Description
- Acceptance Criteria
- Repro Steps (“Repo Steps”)
- System Info
- Comments

When the value contains HTML, convert it to readable Markdown and embed it inline in the dossier (do not wrap raw HTML in a fenced code block).

### Conversion rules

- Preserve meaning and readability over perfect fidelity.
- Prefer Markdown lists/headings/links over raw tags.
- Convert `<br>` to hard line breaks; treat `<p>` as paragraph breaks.
- Convert `<ul>/<ol>/<li>` into Markdown lists.
- Convert `<a href>` into `[text](url)` links.
- Convert `<strong>/<b>` to `**bold**`, `<em>/<i>` to `*italic*`, `<code>` to inline code.
- Strip non-content tags (`<span>`, layout-only `<div>`) unless they contain meaningful text.
- If there are embedded images/attachments in HTML, include their alt/text and the link if present.
- If conversion fails or HTML is malformed, fall back to a best-effort plain-text extraction (still inline).

## Output format (single Markdown file)

Create one file:

- Folder: `WorkItems/` (create if missing)
- Filename: `<WorkItemId>-<Title>.md`

### Filename sanitization

Sanitize `<Title>` for the filename:

- Replace spaces with `-`
- Remove or replace characters not in `[A-Za-z0-9._-]` with `-`
- Collapse repeated `-`
- Trim leading/trailing `-`

### Document structure

Use this structure (keep it consistent):

1) `# <ID>: <Title>`
2) Summary table (Type/State/Effort/CreatedBy/AssignedTo)
3) `## Target Work Item`
4) `## Parent Work Item` (or state “No parent found”)
5) `## Child Work Items` (or state “No children found”)

For each work item section include:

- `### Fields`
  - Description
  - Acceptance Criteria
  - Repro Steps
  - System Info
  - Effort
  - CreatedBy
  - AssignedTo
- `### Comments`

## Safety / correctness rules

- Default to read-only MCP calls.
- If the user asks for updates, confirm the exact changes before calling any write tool.
- Never infer field content that is missing.

## Example request

“Export work item 12345 into a dossier markdown file.”
