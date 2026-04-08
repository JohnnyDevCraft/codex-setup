# Project Modes

This folder centralizes supported project modes for designing and implementing software with structured AI-assisted workflows.

Project modes define:

- The planning and delivery flow to use
- The documents that should exist
- The level of specification required before implementation
- How AI should participate in the workflow
- How project context should be tracked and maintained

## Cross-Mode Implementation Guardrail

Regardless of mode, AI must not implement code unless the requested change is already documented in the active mode’s source-of-truth artifacts and backed by implementation tasks.

If a requested change is new, changed, or refined after prior discussion:

1. Update or create the relevant spec or workflow artifact
2. Generate or update the task breakdown
3. Satisfy the mode’s approval rules
4. Only then begin implementation

## Cross-Mode Spec Immutability Guardrail

Regardless of mode, once implementation begins against a spec and its task breakdown, that implementation scope is fixed.

If the user wants to revise, extend, redesign, or iterate on implemented or in-flight work:

1. Do not mutate the existing implementation spec to absorb the new change
2. Create a new spec or mode-appropriate workflow artifact for the new change
3. Generate a new task breakdown for that new spec
4. Follow the mode’s approval process again
5. Implement from the new spec only

## How To Use Project Modes

- At the start of a new project, ask which project mode to use.
- Read this file and then load the selected mode file from `./modes`.
- Follow the mode’s document structure, flow, and implementation rules.
- Create the project’s root `AGENT.md` immediately and record the selected mode there.
- If a mode includes templates or supporting files, use those files as the starting point for the project.
- Treat the selected mode’s own workflow artifacts as the project source of truth.

## Supported Modes

- [DevCraft](./modes/DevCraft.md)
- [SpecKit](./modes/SpecKit.md)

## Mode Selection Rule

When beginning a new project, agents should ask which mode the project should operate in before scaffolding workflow documents or starting delivery work.

If the user does not specify a mode and local instructions do not force one, ask before proceeding.

## Mode Switching Rule

If a project switches from one mode to another:

1. Identify files and workflow artifacts that belong only to the old mode.
2. Clean up or archive those obsolete mode-specific files.
3. Update the project root `AGENT.md` to record the new active mode.
4. Start the workflow for the new mode immediately.
5. Regenerate or align project documents using the new mode’s templates and rules.

Mode switching should preserve valuable project knowledge, but obsolete workflow scaffolding from the previous mode should not remain as active source-of-truth material.

### Source Of Truth By Mode

- `DevCraft`: DevCraft context files and work-item artifacts are the source of truth.
- `SpecKit`: `constitution.md`, `spec.md`, `plan.md`, `tasks.md`, and related
  SpecKit workflow artifacts are the source of truth.
