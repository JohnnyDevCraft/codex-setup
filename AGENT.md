# AGENT.md

## Purpose

This folder centralizes Codex guidance that is intended to be reused across projects.

This is not a normal application project. It is a shared configuration and documentation workspace for defining how agents should work across repositories.

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

## Agent Workflow Rule

When starting work in a project:

1. Identify the languages and frameworks in use.
2. Identify the architecture or architectures in use.
3. Identify any relevant tools, platforms, or manual systems involved in the work.
4. Read [STD.md](./STD.md).
5. Read [ARCH.md](./ARCH.md).
6. Read [TOOL.md](./TOOL.md).
7. Read each relevant standards file in `./standards`.
8. Read each relevant architecture file in `./Architecture`.
9. Read each relevant tool file in `./tools`.
10. Apply those standards, architecture rules, and tool constraints when designing, implementing, reviewing, and testing code or preparing user-facing tool content.

If a project has its own local standards that extend these shared standards, agents should apply both. When standards conflict, the more specific project-level rule should win unless explicitly instructed otherwise.

If a project has its own local architecture documentation, agents should apply both the shared architecture guidance and the project-specific architecture guidance. When architecture guidance conflicts, the more specific project-level architecture should win unless explicitly instructed otherwise.

If a project has its own local tool documentation or workflow docs, agents should apply both the shared tool guidance and the project-specific tool guidance. When tool instructions conflict, the more specific project-level workflow should win unless explicitly instructed otherwise.

## Scope

This `AGENT.md` applies to work that uses this repository as a shared Codex configuration source.

Project repositories may define additional `AGENT.md` instructions that extend or override this shared guidance.
