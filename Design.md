# Common Designs

This folder centralizes shared design patterns that can be implemented across multiple applications and repositories.

These designs are not visual themes. They are reusable application and system patterns that can be applied repeatedly across projects.

## How To Use Common Designs

- Read this file when a project needs a reusable shared design pattern.
- Load the relevant file in `./designs`.
- Use common designs together with the active project mode, standards, architecture, and tools.
- If a project-specific implementation varies from a common design, document the variation clearly in the project’s architecture or governance files.

## Common Design Index

- [Assistant Chat Command Queue](./designs/Assistant-Chat-Command-Queue.md)

## What A Common Design Should Describe

Each design file should define:

- The purpose of the pattern
- When to use it
- Core components
- Data or queue flow
- Approval and governance boundaries
- Failure handling rules
- Integration points
- Implementation notes

## Maintenance Notes

- Add a new common design when the same architectural or workflow pattern is repeated across projects.
- Update existing designs when the shared pattern changes.
- Prefer concrete operational guidance over abstract theory.
