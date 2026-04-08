# SpecKit Mode

## Purpose

SpecKit is a spec-driven development mode based on GitHub Spec Kit and the broader Spec-Driven Development workflow.

It is designed to make project intent, requirements, planning, and implementation artifacts explicit before major coding work begins, especially when AI agents are involved.

## Baseline

This mode is based on the public GitHub Spec Kit workflow and supporting guidance.

### Primary References

- GitHub Spec Kit repository: [github/spec-kit](https://github.com/github/spec-kit)
- Microsoft Learn module: [Get started with spec-driven development and GitHub Spec Kit](https://learn.microsoft.com/en-us/training/modules/spec-driven-development-github-spec-kit-greenfield-intro/)
- Microsoft developer article: [Diving Into Spec-Driven Development With GitHub Spec Kit](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)

## What SpecKit Emphasizes

- Establish project principles up front
- Define what to build before deciding how to build it
- Turn specifications into living implementation inputs
- Use structured planning and tasks before implementation
- Keep the workflow reviewable and evolvable
- Use active brainstorming early to improve the quality of the constitution and project direction
- Require documented specs, plans, and tasks before implementation begins
- Treat implemented specs as fixed for the duration of that implementation cycle

## Core Flow

Based on the public Spec Kit workflow, the typical sequence is:

1. Initialize the project for Spec Kit
2. Establish the project constitution through active brainstorming
3. Create the feature or project specification
4. Clarify underspecified areas when needed
5. Produce the technical plan
6. Generate implementation tasks
7. Implement from the task breakdown

Implementation must not begin unless the requested work is already reflected in the active SpecKit artifacts and backed by tasks.

Once implementation begins from a SpecKit task breakdown, any follow-up change or iteration should go back through a new specification flow rather than extending the in-flight implemented scope.

## Constitution Brainstorming Flow

In this workspace, SpecKit constitution work is not a passive note-taking step. It is an active collaborative design phase.

During the constitution phase, AI should:

1. Ask proactive questions to uncover goals, constraints, risks, and assumptions.
2. Challenge vague or weak thinking instead of merely recording it.
3. Point out flaws, contradictions, missing considerations, and likely failure modes in the proposed design.
4. Offer practical alternatives and improvements when a weakness is identified.
5. Help shape product direction, system behavior, and user experience expectations early.
6. Drive the conversation toward a clearer operating constitution before downstream specification work begins.

### Constitution Topics To Explore

- Who the users are
- What problem the project solves
- Why the solution is needed now
- What quality bar defines success
- What constraints the project must respect
- What operational or security rules matter
- What user-experience principles should govern the product
- What tradeoffs are acceptable and unacceptable

### AI Posture During Constitution Work

- Be proactive rather than passive
- Be constructively critical rather than agreeable by default
- Surface risks early
- Suggest solutions when calling out a weakness
- Assist in UX design, UX tradeoff evaluation, and workflow shaping
- Push for clarity before the project moves deeper into specification and planning

## Common SpecKit Commands

Spec Kit exposes a family of commands around the development lifecycle. Public references describe these core commands:

- `/speckit.constitution`
- `/speckit.specify`
- `/speckit.plan`
- `/speckit.tasks`
- `/speckit.implement`

Public references also describe optional supporting commands such as:

- `/speckit.clarify`
- `/speckit.analyze`
- `/speckit.checklist`

For Codex-oriented skill usage, public Spec Kit documentation also references skill-style invocation when installed that way.

## Agent Orchestration In SpecKit

In this workspace, the user should not need to manually tell the AI when to change behavior between SpecKit phases.

The AI should infer the correct SpecKit phase from the current state of the conversation, the project artifacts that already exist, and the user’s immediate goal.

### Phase-Driven Agent Behavior

The AI should shift its behavior automatically across these modes of work:

1. Constitution behavior
2. Specification behavior
3. Clarification behavior
4. Planning behavior
5. Task-generation behavior
6. Analysis behavior
7. Implementation behavior

These are not separate user-invoked personalities in this workspace. They are expected operating modes that the AI should move through fluidly.

### How AI Should Infer The Active Phase

The AI should determine the current SpecKit phase by looking at:

- What the user is asking for now
- Which SpecKit artifacts already exist
- Whether the constitution is mature enough
- Whether the specification is complete enough to plan
- Whether the plan is complete enough to generate tasks
- Whether the tasks are complete enough to implement
- Whether inconsistencies or gaps require clarification or analysis before moving forward

### Expected Automatic Transitions

- If the constitution is missing or weak, move into constitution behavior
- If the constitution exists but the feature definition is incomplete, move into specification behavior
- If the spec or constitution contains ambiguity, move into clarification behavior
- If the spec is approved and technically ready, move into planning behavior
- If the plan is approved, move into task-generation behavior
- If tasks, plans, or specs appear incomplete, use checklist behavior to confirm completeness
- If tasks exist but alignment is uncertain, move into analysis behavior
- If tasks are approved and the user asks to build, move into implementation behavior

### Constitution Behavior

- Drive brainstorming proactively
- Ask guiding questions
- Surface hidden assumptions
- Challenge weak ideas
- Propose better alternatives
- Help define UX principles and product direction

### Specification Behavior

- Convert the constitution and product intent into concrete feature or project specifications
- Focus on what should be built and why
- Keep the spec user-centered and outcome-centered

### Clarification Behavior

- Identify ambiguity, inconsistency, or missing decisions
- Ask targeted questions that unblock planning
- Narrow open decisions enough to continue the workflow
- Use clarification proactively when the constitution and a feature spec do not line up cleanly

### Planning Behavior

- Translate the approved specification into technical design and execution strategy
- Identify architecture impacts, dependencies, risks, and sequencing
- Make implementation tradeoffs visible

### Task-Generation Behavior

- Break the approved plan into actionable work items
- Organize work in a logical order
- Make tasks concrete enough for implementation

### Checklist Behavior

- Use checklist thinking to verify that a constitution, specification, plan, or task set is complete enough for the next phase
- Surface missing sections, unaddressed risks, unresolved decisions, or absent acceptance criteria
- Apply checklist review proactively when a document appears mature but may still be incomplete

### Analysis Behavior

- Check consistency across constitution, spec, plan, and tasks
- Identify missing work, contradictions, or drift
- Recommend corrections before implementation continues
- Ensure features remain coherent with the project constitution and with other approved features
- Detect when a new feature introduces standards, UX behavior, or operational rules that conflict with constitution-level decisions

### Implementation Behavior

- Execute from the approved plan and task list
- Keep progress visible
- Avoid skipping back into speculative design unless a blocker requires it
- Do not implement undocumented requests; route them back through specify, clarify, plan, and tasks first when needed
- Do not absorb new scope into the currently implemented spec once implementation is underway; create a new spec flow for the new change

### Agent Conduct Rule

- The AI should not wait for the user to say “switch agents” or “move to the next phase”
- The AI should guide the user to the next correct phase when the current one is sufficiently complete
- If a phase transition is risky or premature, the AI should say so clearly and explain why
- When the AI identifies a better next step, it should recommend it directly instead of waiting passively
- The AI should proactively trigger clarification, analysis, or checklist behavior when coherence or completeness is at risk

## Expected Artifacts

The public Spec Kit flow commonly produces or relies on artifacts such as:

- `constitution.md`
- `spec.md`
- `plan.md`
- `tasks.md`

These artifacts act as the structured context for implementation.
They are also the governing source of truth for project intent, requirements,
planning, and implementation sequencing while the project is operating in
`SpecKit` mode.

## AI Responsibilities In SpecKit

- Confirm the project should operate in `SpecKit` mode
- Create the project root `AGENT.md` immediately and record that `SpecKit` is the active mode
- Treat SpecKit artifacts as the project source of truth and avoid maintaining
  parallel DevCraft-style context files unless the user explicitly asks for
  cross-mode documentation
- Follow the constitution -> specify -> plan -> tasks -> implement sequence
- Do not implement code unless the requested change is already documented in SpecKit artifacts and backed by implementation tasks
- Infer the correct SpecKit phase automatically from context and artifact maturity
- Transition between SpecKit phase behaviors without waiting for the user to explicitly request an agent switch
- Treat the constitution step as an active brainstorming and design phase
- Ask proactive questions during constitution work instead of waiting for perfect input
- Point out flaws in designs, assumptions, and thought processes
- Offer solutions and alternative approaches when identifying problems
- Help design the UX and call out user-flow weaknesses early
- Treat specification files as living workflow artifacts
- Avoid skipping directly to implementation when core artifacts are missing
- Use clarification and analysis steps when requirements are underspecified or inconsistent
- Use checklist reviews proactively when a phase appears complete but may still be missing important elements
- Maintain coherence between constitution-level decisions, feature-level decisions, and the evolving set of approved work
- If the user changes the requested behavior, design, or scope, update the relevant SpecKit artifacts and tasks before coding the change
- If the user changes the requested behavior, design, or scope after implementation has started, create a new SpecKit change flow instead of extending the in-flight implemented spec

## When To Use

- The team wants a formal spec-driven workflow
- AI agents are expected to implement from structured planning artifacts
- Requirements, architecture, and task planning should be explicit before major coding begins
- The project benefits from constitution-style operating principles and feature-level implementation planning
- The team wants AI to actively improve early design thinking rather than only document it

## Mode Switching

If switching away from SpecKit:

- Clean up or archive active SpecKit-only workflow files that no longer serve as the source of truth
- Preserve useful requirements and planning knowledge in the new mode’s structure
- Update the project root `AGENT.md` to record the new mode

## Notes

- The exact initialization and command surface can vary by environment and agent integration.
- Use the project’s actual Spec Kit install and command exposure if it already exists.
- If the project is not yet initialized for Spec Kit, align setup with the current public Spec Kit guidance and the project’s AI tooling.
- In this workspace, the constitution phase should include active brainstorming, critique, and UX assistance even if a base Spec Kit install treats constitution more narrowly.
- In this workspace, SpecKit phase changes should feel automatic and conversational rather than requiring manual agent-selection prompts.
- In this workspace, `clarify`, `analyze`, and `checklist` behavior should be triggered proactively whenever completeness or coherence is in doubt.
- In this workspace, coding must always follow documented SpecKit artifacts and task breakdowns; undocumented changes go back through the workflow before implementation.
- In this workspace, once implementation has started from a SpecKit artifact set, iteration or redesign must flow through a new spec/task cycle rather than mutating the implemented one.
