# AGENT.md

## Purpose

This folder centralizes Codex guidance that is intended to be reused across projects.

This is not a normal application project. It is a shared configuration and documentation workspace for defining how agents should work across repositories.

## Shared Rule Update Requirement

If the user says to update the core rules, shared rules, or cross-project guidance, agents should apply those updates in this repository so the changes can be reused across projects.

This includes updates to shared:

- Modes
- Standards
- Architecture guidance
- Tool definitions
- Common designs
- Templates
- Shared `AGENT.md` workflow rules

Agents should treat this repository as the source of truth for reusable Codex operating guidance.

## Coding Guardrail Requirement

Agents must not implement code that is not already represented in project documentation.

Before coding begins, there must be:

- A documented spec or mode-appropriate workflow artifact describing the change
- A task list or implementation task breakdown that the coding work can execute against
- Approval to proceed according to the active project mode

This rule applies even when the user asks for a small tweak, refinement, redesign, or follow-up change after seeing a previous implementation.

If the user asks to change behavior, appearance, structure, or implementation and that change is not already documented:

1. Do not code it yet
2. Create or update the relevant spec or workflow artifact first
3. Generate or update the tasks for that change
4. Then proceed only after the active mode’s approval rules are satisfied

## Implemented Spec Immutability Rule

Once implementation begins against a spec and its tasks, that spec should be treated as fixed for that implementation cycle.

After a feature, task set, or mode-specific implementation artifact has moved into implementation:

- Do not add new scope to that same spec in order to continue coding
- Do not append new implementation tasks to extend the original spec’s scope
- Do not treat iteration, redesign, or follow-up changes as part of the old implemented spec

If the user wants to change, refine, redesign, or extend something after implementation has started or completed:

1. Create a brand new spec or mode-appropriate workflow artifact for that new change
2. Generate a new task list for that new spec
3. Follow the active mode’s approval process
4. Implement the new change from the new spec only

## Response Style Requirement

Agents should prefer option-based responses when the workflow reaches a decision point.

The goal is to let the user move quickly by selecting from short, clear options instead of reading long exploratory responses.

### Option-Based Response Rules

- Present decisions as short numbered options whenever practical.
- Use clickable file links when referencing local mode, standards, architecture, or tool documents.
- Keep options concise and action-oriented.
- Put the recommended option first when there is an obvious best next step.
- Use free-form explanation only when the user needs deeper context or when the decision is too nuanced for a short option list.

### Good Use Cases For Option-Based Responses

- Selecting a project mode
- Selecting a branching model
- Choosing whether work starts from a work item
- Choosing between supported architectures
- Choosing between supported tools
- Choosing the next workflow phase
- Confirming whether to design, clarify, analyze, plan, or implement
- Choosing a common design pattern

### Example Pattern

1. [Use DevCraft](/Users/john/codex-setup/modes/DevCraft.md)
2. [Use SpecKit](/Users/john/codex-setup/modes/SpecKit.md)

Agents should use this style by default for intake, branching workflow steps, and structured project decisions.

## Project Mode Requirement

When starting a new project, agents must begin by asking which project mode the work should use.

Supported modes are defined in [MODES.md](./MODES.md) and the files in `./modes`.

After the user selects a mode:

1. Read [MODES.md](./MODES.md).
2. Read the selected mode file in `./modes`.
3. Create the project root `AGENT.md` immediately.
4. Record the active mode in the project root `AGENT.md`.
5. Start the workflow for the selected mode at once.

If the project later switches modes:

1. Clean up or archive active files that belonged only to the old mode.
2. Update the project root `AGENT.md` to record the new active mode.
3. Start the new mode’s workflow immediately.
4. Align the project’s active workflow files with the new mode’s structure.

## New Project Intake

When starting a brand new project, or when adding Codex to an existing project for the first time, agents should follow this intake flow immediately.

### Intake Step 1: Select The Project Mode

Ask which mode the project should use:

1. [DevCraft](./modes/DevCraft.md)
2. [SpecKit](./modes/SpecKit.md)

If the project already has an established workflow, first detect whether `SpecKit` or `DevCraft` is already being used in the project.

If one of those modes is already clearly present:

- Do not ask the user to re-select the mode unless the project state is ambiguous
- Record the detected mode in the project root `AGENT.md`
- Treat the existing workflow artifacts as the current project framework
- Do not overwrite the project’s existing configuration or workflow files

If no supported mode is clearly present, ask the user which mode should become the source-of-truth workflow.

### Intake Step 2: Create The Project Root AGENT File

Create the project root `AGENT.md` immediately.

Record:

- The active mode
- The project name
- The current status
- The branching model if the mode uses one
- The master branch
- Initial project context as it becomes known

If the project already exists and already uses `SpecKit` or `DevCraft`:

- Create the project root `AGENT.md` as an integration layer for Codex
- Note the workflow mode already in use
- Do not replace or rewrite the project’s existing workflow artifacts unless the user explicitly asks for a migration or cleanup

### Intake Step 3: Load Shared Guidance

Read:

- [MODES.md](./MODES.md)
- [STD.md](./STD.md)
- [ARCH.md](./ARCH.md)
- [TOOL.md](./TOOL.md)
- [Design.md](./Design.md)

Then load:

- The selected mode file from `./modes`
- The relevant standards files from `./standards`
- The relevant architecture files from `./Architecture`
- The relevant tool files from `./tools`
- The relevant common design files from `./designs`

### Intake Step 4: Determine Project Context

Identify:

- Languages and frameworks
- Architecture or architectures
- Relevant tools and manual systems
- Relevant common design patterns
- Work-item storage and tooling
- Collaboration model
- Security concerns
- Governing rules
- Ubiquitous language

### Intake Step 5: Start The Selected Mode

For `DevCraft`:

- Start the project setup flow
- Create the DevCraft context files
- Capture project purpose, users, rules, security concerns, work-item model, collaboration model, branching model, and master branch

For `SpecKit`:

- Start the constitution phase immediately
- Use proactive brainstorming, clarification, analysis, checklist, and UX design support
- Drive toward a coherent constitution before moving deeper into specification and planning
- Treat the active `SpecKit` artifacts as the project source of truth
- Avoid creating or maintaining DevCraft-only context documents unless the user explicitly wants cross-mode documentation

### Intake Step 6: Align Existing Repositories

If Codex is being added to an existing project:

- Read the existing project documents first
- Detect whether `SpecKit` or `DevCraft` is already being used
- If one is already in use, create or update the project root `AGENT.md` to record that fact
- Do not overwrite existing project configuration that already supports the detected workflow
- Move directly into working within the existing framework
- If no supported mode is detected, confirm the workflow mode with the user and align the project to that mode

## Standards Requirement

Before making code changes in any project, agents must review the shared standards defined in [STD.md](./STD.md).

Agents must then read the standards files that apply to the languages and frameworks used in the target project.

Examples:

- A Laravel project should load [PHP](./standards/PHP.md) and [Laravel](./standards/Laravel.md).
- An ASP.NET Core project should load [C#](./standards/CSharp.md) and [ASP.NET Core](./standards/ASP.Net%20Core.md).
- A TypeScript frontend should load [TypeScript](./standards/Typescript.md).
- A JavaScript utility or script should load [JavaScript](./standards/Javascript.md).

## Tool Requirement

When a project depends on a named external tool, internal tool, console tool, MCP tool, or manual platform workflow, agents must review the shared tool catalog in [TOOL.md](./TOOL.md) and load the relevant tool file from `./tools` when one exists.

Manual tools are especially important because agents may be asked to generate content for them even when the agent cannot operate the tool directly.

## Tool Usage Rules

Agents must treat tool documentation as operational guidance, not optional reference material.

When a tool is relevant to the work:

1. Read [TOOL.md](./TOOL.md).
2. Read the relevant tool file in `./tools`.
3. Identify the tool category:
   - `MCP Tool`
   - `Local Console`
   - `Manual Tool`
4. Follow the documented dependencies, install instructions, commands, inputs, outputs, and constraints before using the tool or preparing content for it.

### MCP Tool Usage

- Use the documented MCP workflow and JSON shape when interacting with the tool.
- Do not invent MCP payloads when the tool file defines the expected structure.
- Respect authentication, rate limits, and output constraints documented in the tool file.

### Local Console Tool Usage

- Verify dependencies and environment setup before running commands.
- Follow the documented install and activation workflow.
- Prefer the documented commands over ad hoc alternatives unless there is a strong reason to diverge.
- If the environment is missing or broken, report the gap clearly and do not pretend the tool is ready.

### Manual Tool Usage

- Do not assume direct tool access.
- Use the tool file to prepare the exact content the user needs for that tool.
- Respect field purposes, formats, limits, tone, and output expectations.
- Make it clear when AI is preparing inputs for a human rather than operating the system directly.

### Tool Selection Rule

- If multiple tools could apply, choose the one that best matches the project workflow and the user’s requested outcome.
- If a project-specific tool document exists, use it together with the shared tool definition.
- If no tool file exists yet for a relevant tool, create or request one when the tool is important to ongoing work.

## Common Design Requirement

When a project uses a reusable system pattern that can apply across multiple applications, agents must review [Design.md](./Design.md) and load the relevant file from `./designs`.

Common designs should be used for repeatable patterns such as queue-backed assistant workflows, shared orchestration flows, and other implementation patterns that are broader than a single project.

## Agent Workflow Rule

When starting work in a project:

1. Identify the active project mode.
2. Identify the languages and frameworks in use.
3. Identify the architecture or architectures in use.
4. Identify any relevant tools, platforms, or manual systems involved in the work.
5. Read [MODES.md](./MODES.md).
6. Read the active mode file in `./modes`.
7. Read [STD.md](./STD.md).
8. Read [ARCH.md](./ARCH.md).
9. Read [TOOL.md](./TOOL.md).
10. Read [Design.md](./Design.md).
11. Read each relevant standards file in `./standards`.
12. Read each relevant architecture file in `./Architecture`.
13. Read each relevant tool file in `./tools`.
14. Read each relevant common design file in `./designs`.
15. Apply the selected mode, standards, architecture rules, tool constraints, and common design guidance when designing, implementing, reviewing, and testing code or preparing user-facing tool content.

### Mode-Specific Source Of Truth Rule

- In `SpecKit` mode, the governing project artifacts are the active `constitution.md`,
  `spec.md`, `plan.md`, `tasks.md`, and other SpecKit workflow documents produced
  by the selected mode.
- In `SpecKit` mode, agents should not invent parallel DevCraft-style context
  files as competing sources of truth unless the user explicitly asks for them.
- In `DevCraft` mode, the DevCraft project context documents remain the source
  of truth for that workflow.

During implementation:

1. Use tool documentation to decide whether the work is direct execution, environment setup, or content preparation.
2. Follow documented commands and workflows before improvising.
3. Do not code against undocumented intent; ensure there is an approved spec and implementation tasks first.
4. Respect tool-specific input limits and output formats.
5. For Laravel modular monolith work, apply new migrations immediately after creating them so the schema stays ready for downstream development.
6. Update tool documentation when the shared workflow materially changes.
7. Update shared guidance in this repository when the user asks for a cross-project rule change.

## Change Tracking Requirement

Regardless of the active project mode, whenever Codex creates or modifies a file during implementation it must produce a detailed record of what changed and why.

This requirement applies in every mode. The location and format of the record depends on the active mode:

- **DevCraft**: Record changes in `results.md` inside the feature spec subfolder (see [DevCraft mode](./modes/DevCraft.md)).
- **SpecKit**: Record changes in a `results.md` file stored alongside or inside the relevant spec artifacts (see [SpecKit mode](./modes/SpecKit.md)).
- **Any future mode**: Must also use a `results.md` per spec or per unit of work to track file-level changes and the reasons behind each change.

### What The Change Record Must Include

For every file that is created or modified during a unit of implementation work:

- The file path
- A description of what changed in that file
- The reason why that change was made

This record must be written at the end of implementation, before the work is considered complete.

## Core Rules That Must Remain Visible

- Shared guidance changes should be written back to this repository when the user asks to update core rules.
- Common reusable system patterns should be captured through [Design.md](./Design.md) and `./designs`.
- Code should not be implemented unless it is backed by documented specs and implementation tasks.
- Once implementation begins, changes and iterations must move to a new spec rather than extending the active implemented spec.
- Laravel modular monolith workflows should apply migrations immediately after creating them during development.
- DevCraft work items should use typed feature specs with `Feature`, `Bug`, `Enabler`, or `Task` types.
- In `SpecKit` mode, SpecKit workflow artifacts are the source of truth and should not be shadowed by parallel DevCraft context files.
- When onboarding an existing project, detect whether `SpecKit` or `DevCraft` is already in use and do not overwrite the project’s existing workflow configuration.
- If a project uses a `theme/` subfolder, its `THEME.md` should stay aligned to those assets and Tailwind input CSS files.
- DevCraft projects should keep root context files current after completed work.
- Every mode must produce a `results.md` per spec or per unit of work that records files changed, what changed, and why.

If a project has its own local standards that extend these shared standards, agents should apply both. When standards conflict, the more specific project-level rule should win unless explicitly instructed otherwise.

If a project has its own local architecture documentation, agents should apply both the shared architecture guidance and the project-specific architecture guidance. When architecture guidance conflicts, the more specific project-level architecture should win unless explicitly instructed otherwise.

If a project has its own local tool documentation or workflow docs, agents should apply both the shared tool guidance and the project-specific tool guidance. When tool instructions conflict, the more specific project-level workflow should win unless explicitly instructed otherwise.

## Scope

This `AGENT.md` applies to work that uses this repository as a shared Codex configuration source.

Project repositories may define additional `AGENT.md` instructions that extend or override this shared guidance.
