# Project Modes

This folder centralizes supported project modes for designing and implementing software with structured AI-assisted workflows.

Project modes define:

- The planning and delivery flow to use
- The documents that should exist
- The level of specification required before implementation
- How AI should participate in the workflow
- How project context should be tracked and maintained

## How To Use Project Modes

- At the start of a new project, ask which project mode to use.
- Read this file and then load the selected mode file from `./modes`.
- Follow the mode’s document structure, flow, and implementation rules.
- Create the project’s root `AGENT.md` immediately and record the selected mode there.
- If a mode includes templates or supporting files, use those files as the starting point for the project.

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

## New Mode Authoring Rule

When a new mode is added to this repository, it must include change tracking support:

- The mode must require a `results.md` per spec or per unit of work after implementation.
- The `results.md` must record every file that was created or modified, what changed in each file, and why the change was made.
- The mode folder should include a `results.template.md` in its `./templates` subfolder as a starting point.

This requirement exists so that every mode produces a consistent, auditable implementation record regardless of which mode is active.
