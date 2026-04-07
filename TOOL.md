# Tool Catalog

This folder centralizes reusable tool definitions across projects.

## How To Use These Tool Files

- Read this file when adding a new tool to the shared catalog.
- Create one markdown file per tool in `./tools`.
- Use the tool file as the source of truth for how the tool is used, what inputs it needs, and whether AI can interact with it directly.
- When working on a project, agents should load the relevant tool documents for any external system, manual workflow, MCP integration, console utility, or export target involved in the work.

## Tool Index

- [Image Gen](./tools/Image-Gen.md)
- [Theme Maker](./tools/Theme-Maker.md)

## Tool Categories

Each tool must be categorized as one of the following:

- `MCP Tool`
- `Local Console`
- `Manual Tool`

### Category Meaning

- `MCP Tool`: AI can interact with the tool through an MCP integration.
- `Local Console`: AI can interact with the tool through shell commands or a local CLI.
- `Manual Tool`: AI cannot directly operate the tool, but can prepare content, prompts, copy, metadata, instructions, or structured inputs for a human to use in the tool.

## Standard Tool Document Structure

Each tool file should include at minimum:

- Name
- Category
- URL
- Tool Description
- Primary Use Cases
- Dependencies
- Install Instructions
- Tool Commands
- MCP JSON
- Tool Inputs
- Outputs
- AI Usage Notes
- Constraints and Limits
- Authentication or Access Requirements
- Output or Deliverables
- Example Requests

## Outputs Section

Each tool file must include an `Outputs` section.

The `Outputs` section should describe:

- What the tool produces
- The output artifact type or format
- The structure of the output when known
- Any packaging, naming, or content rules
- How the output is expected to be used downstream

For manual tools, the `Outputs` section should describe the final artifact produced by the tool, even when AI is only responsible for preparing input content or guidance.

## Dependencies Section

Each tool file must include a `Dependencies` section.

The `Dependencies` section should describe:

- Required software
- Required services or accounts
- Runtime or platform prerequisites
- Related tools, libraries, or systems the tool depends on

If a tool has no meaningful dependency information yet, state that explicitly instead of omitting the section.

## Install Instructions Section

Each tool file must include an `Install Instructions` section.

The `Install Instructions` section should describe:

- How the tool is installed or accessed
- Any required environment setup
- Login or configuration requirements
- Whether installation is not applicable for manual or hosted tools

If installation is not applicable, state that clearly.

## New Tool Intake Workflow

When a user asks to add a new tool to the system, capture the following information before or while creating the tool file.

### Required Questions

1. What is the tool name?
2. What kind of tool is it: `MCP Tool`, `Local Console`, or `Manual Tool`?
3. What is the primary URL or home page for the tool?
4. What is the short description of what the tool does?
5. How is the tool used in our projects?
6. What dependencies does the tool have?
7. How is the tool installed, configured, or accessed?
8. What commands can AI run, if any?
9. Does it have MCP access? If yes, what JSON shape or MCP call details matter?
10. What inputs might AI be asked to prepare?
11. For each input, what is it for, what format does it require, and what limits apply?

### Helpful Follow-Up Questions

1. Does the tool require login, API keys, local installation, or special environment setup?
2. Are there important output formats, export files, naming rules, or validation rules?
3. Are there brand, legal, marketing, or platform-specific content constraints?
4. Should the tool file include reusable prompt templates, content templates, or examples?
5. What mistakes should agents avoid when preparing content for this tool?

## Suggested Additional Metadata

When useful, also capture:

- Owner or vendor
- Pricing tier assumptions
- Environment requirements
- Supported platforms
- Rate limits
- Approval requirements
- Human review checkpoints
- Links to official docs

## File Naming Rule

Store each tool file in `./tools` using a readable Pascal-cased or title-style filename with hyphens where needed.

Example:

- `Theme-Maker.md`
- `App-Store-Connect.md`
- `Stripe-Dashboard.md`

## Maintenance Notes

- Update tool files when workflows, limits, or required inputs change.
- Prefer concrete constraints over vague descriptions.
- If a tool is manual, document exactly what kind of text or structured content AI should generate for the user.
