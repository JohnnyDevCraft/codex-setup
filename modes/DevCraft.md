# DevCraft Mode

## Purpose

DevCraft is the custom project mode defined by this workspace’s operating rules. It is a documentation-first, approval-gated development workflow designed to keep project context, architecture, theme direction, data model decisions, and feature intent explicit before implementation work begins.

## When To Use

- The project should follow the custom workflow defined in this shared Codex setup
- The team wants documentation to act as the source of truth
- Features should be designed and approved before implementation
- The project benefits from durable context files and evolving feature specs

## Core Principles

- Documentation is part of the product, not an afterthought.
- New work starts with context and design, not immediate implementation.
- Features, bugs, enablers, and tasks are tracked through living feature specifications.
- Project context files are maintained as ongoing source-of-truth documents.
- Implementation follows explicit approval.
- Testing is required for completed work.

## Branching Models

DevCraft supports two branching models.

### Simple Branching

Use `Simple Branching` for single-user development.

- One master branch is used for active development
- Do not create feature branches for each feature
- Approved features are implemented directly on the master branch
- This model is intended for solo development where repository coordination overhead should stay low

### Advanced Branching

Use `Advanced Branching` for team development or any workflow that benefits from isolated feature branches.

- A master branch acts as the source branch for new work
- Each approved feature, bug, task, or enabler is implemented on its own branch
- Use this naming convention:
  - `[username]/[bug|feature|task|enabler]/[ticket-id]-[ai_generated_description_up_to_55_chars]`
- This model is intended for shared repositories and multi-person collaboration

## Core Flow

### Project Setup Flow

1. Confirm that the project will operate in `DevCraft` mode.
2. Create the project root `AGENT.md` immediately and record that the active mode is `DevCraft`.
3. Ascertain the purpose of the project:
   - Who will use it
   - Why it is needed
   - The ubiquitous language model
   - What rules govern its operation
   - What security concerns need to be remembered
4. Ascertain the project languages, frameworks, and architecture models.
5. Ascertain where work items will be stored and whether tooling exists to interact with those work items.
6. Ascertain how many people will be working in the same repository and for what purpose.
7. Choose the branching model:
   - `Simple Branching`
   - `Advanced Branching`
8. Identify the branch name that will act as the master branch for the project and store it in the project root `AGENT.md`.
9. Store the branching model in the project root `AGENT.md`.
10. Create the DevCraft context files in the project root:
   - `AGENT.md`
   - `README.md`
   - `GOV.md`
   - `MODEL.md`
   - `THEME.md`
   - `ARCH.md`
   - `DISCOVERY.md`
11. Use the templates in [`./DevCraft/templates`](./DevCraft/templates) as the starting point.
12. Fill the context files with the best known project information before feature implementation begins.
13. If a shared common design pattern applies, load [Design.md](../Design.md) and the relevant file in `../designs`.

### Existing Project Flow

1. Read all project context files at the start of the thread.
2. Identify the active standards, architecture, tools, and project context.
3. Identify the active mode and confirm that the project documents still align to that mode.
4. Update the context files as part of every completed request.

### Feature Spec Flow

1. Determine whether the work starts from a work item.
2. If the work starts from a work item, include a work-item section in the spec that captures the relevant work-item details.
3. Generate a feature spec for the feature or work item to be implemented.
4. Set the feature spec type:
   - `Feature`
   - `Bug`
   - `Enabler`
   - `Task`
5. Brainstorm the feature with the user to refine the feature spec.
6. Analyze the codebase when needed to understand the changes that will need to occur.
7. Create implementation phases based on goals and feature design.
8. Once phases are approved, create the tasks for each phase.
9. The human developer approves the feature spec.
10. Do not implement code until the feature spec is approved.
11. Before implementation begins:
   - If using `Simple Branching`:
     - Pull the latest version of the project’s master branch
     - Implement directly on the master branch
   - If using `Advanced Branching`:
     - Pull the latest version of the project’s master branch
     - Create a feature branch from the master branch
     - Use this naming convention:
       - `[username]/[bug|feature|task|enabler]/[ticket-id]-[ai_generated_description_up_to_55_chars]`
12. After the active implementation branch is ready, implement the feature and keep task status updated as each step is completed.
13. After implementation is complete:
   - Generate a list of files changed
   - For each file, record the changes made and why those changes were made
14. Commit the changes to the current branch and push to `origin`.

### Feature Flow

1. Create or update a feature spec in `./features`.
2. Use the filename format `<id>-<FeatureNamePascalCased>.md`.
3. Set the spec type to `Feature`, `Bug`, `Enabler`, or `Task`.
4. Keep the feature status explicit:
   - `In Design`
   - `Rejected`
   - `Approved`
   - `Complete`
5. During design, define the feature plan in phases.
6. During planning, define the tasks for each phase as checklist items.
7. The `Plan` and `Tasks` sections should be reviewed and approved with the rest of the feature spec when possible.
8. If the feature is linked to a work item, capture the work-item details in the feature spec.
9. Do not implement code until the feature is approved.
10. During implementation, check tasks off in the spec as they are completed.
11. When implementation is complete, append the implemented changes and reasons to the feature spec.

## Required Project Documents

These are the default DevCraft context files for a new project:

- `AGENT.md`
- `README.md`
- `GOV.md`
- `MODEL.md`
- `THEME.md`
- `ARCH.md`
- `DISCOVERY.md`

## Template Files

Use the templates in [`./DevCraft/templates`](./DevCraft/templates).

### Available Templates

- [AGENT.template.md](./DevCraft/templates/AGENT.template.md)
- [README.template.md](./DevCraft/templates/README.template.md)
- [GOV.template.md](./DevCraft/templates/GOV.template.md)
- [MODEL.template.md](./DevCraft/templates/MODEL.template.md)
- [THEME.template.md](./DevCraft/templates/THEME.template.md)
- [ARCH.template.md](./DevCraft/templates/ARCH.template.md)
- [DISCOVERY.template.md](./DevCraft/templates/DISCOVERY.template.md)
- [Feature-Spec.template.md](./DevCraft/templates/Feature-Spec.template.md)

## AI Responsibilities In DevCraft

- Ask for the active mode when a new project begins.
- Create the project root `AGENT.md` immediately and record `DevCraft` as the active mode.
- Capture the project setup details required by the Project Setup Flow.
- Create and maintain the project context files.
- Determine and record whether the project uses `Simple Branching` or `Advanced Branching`.
- Load shared design patterns from [Design.md](../Design.md) when they apply to the project.
- Start new work in design mode by default.
- Create or update typed feature specifications before implementation.
- Capture work-item details when work begins from a tracked item.
- Brainstorm feature scope with the user before implementation.
- Analyze the codebase when needed before finalizing implementation phases and tasks.
- Add phased plans and implementation tasks to feature specifications during the design process.
- Use checklist task items so progress can be tracked directly inside the spec.
- Avoid implementation until the feature or bug is approved.
- Before approved implementation starts, follow the branching flow defined by the project:
  - `Simple Branching`: update from master and implement on master
  - `Advanced Branching`: update from master and create the feature branch using the DevCraft naming convention
- Keep task status current while implementing.
- Record changed files, per-file changes, and reasons in the completed feature spec.
- Keep the context files current after each completed request.
- Run required testing before marking implementation complete.

## Implementation Rules

- Default mode is documentation and design, not immediate implementation.
- New features begin with a feature spec in `./features`.
- Bugs, enablers, and tasks also use the feature spec format in `./features`.
- Feature specs should include a `Plan` section and a `Tasks` section.
- Feature specs should define a spec type of `Feature`, `Bug`, `Enabler`, or `Task`.
- Feature specs should include a work-item section when the work starts from a tracked work item.
- Feature specs should include a codebase analysis section when analysis is needed to shape implementation.
- Plans should be phased when that improves implementation clarity.
- Tasks should be written as markdown checkboxes so they can be marked complete during delivery.
- Before implementation of an approved feature, follow the project’s selected branching model.
- `Simple Branching` uses only the master branch and is intended for single-user development.
- `Advanced Branching` creates one branch per approved item and uses the naming convention `[username]/[bug|feature|task|enabler]/[ticket-id]-[ai_generated_description_up_to_55_chars]`.
- After implementation, record changed files and the reasons for each file change in the feature spec.
- After creating a new Laravel migration, apply it immediately before continuing feature work.
- If a project uses a `theme/` subfolder, keep `THEME.md` aligned to the assets and Tailwind input CSS stored there.
- If the project uses assistant-triggered system actions, prefer the shared Assistant Chat Command Queue common design unless the project documents a stronger alternative.
- Context files must be updated as the final step of each completed request.

## Testing Expectations

- Every feature should include unit testing for code.
- Web-based features should include Playwright UI testing.
- All relevant tests should be run after implementation.

## Repository Structure Guidance

- Laravel projects should live in `./laravel-<name>`
- .NET solutions should live in `./Net-<Name>`
- Angular projects should live in `./ng-app`
- Xcode projects should live in `./xcode-<name>`

## Mode-Specific Notes

- Theme assets may be stored in a project `theme/` subfolder and should be reflected in `THEME.md`.
- When adding chat-driven system actions, use a queued command approach with background processing and chat-thread updates.
- Shared reusable patterns should be captured through [Design.md](../Design.md) and the files in `../designs`.

## Mode Switching

If switching away from DevCraft:

- Remove or archive DevCraft-only active workflow files that no longer apply
- Preserve useful project knowledge by migrating it into the new mode’s structure
- Update the project root `AGENT.md` to record the new mode

## References

- [Project Modes](../MODES.md)
- [Template Files](./DevCraft/templates)
