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

## Agent Workflow Rule

When starting work in a project:

1. Identify the languages and frameworks in use.
2. Read [STD.md](./STD.md).
3. Read each relevant standards file in `./standards`.
4. Apply those standards when designing, implementing, reviewing, and testing code.

If a project has its own local standards that extend these shared standards, agents should apply both. When standards conflict, the more specific project-level rule should win unless explicitly instructed otherwise.

## Scope

This `AGENT.md` applies to work that uses this repository as a shared Codex configuration source.

Project repositories may define additional `AGENT.md` instructions that extend or override this shared guidance.
