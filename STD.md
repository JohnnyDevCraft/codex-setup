# Coding Standards

This folder centralizes coding standards that can be reused across projects.

## How To Use These Standards

- Start with the language standard for the code being written.
- Add the relevant framework standard when a framework-specific file applies.
- When two standards overlap, the more specific standard wins.
- Project-specific standards may extend these documents, but should avoid contradicting them without a clear reason.

## Standards Index

### Languages

- [C# Standards](./standards/CSharp.md)
- [TypeScript Standards](./standards/Typescript.md)
- [JavaScript Standards](./standards/Javascript.md)
- [Python Standards](./standards/Python.md)
- [Go Standards](./standards/GoLANG.md)
- [PHP Standards](./standards/PHP.md)

### Frameworks

- [Laravel Standards](./standards/Laravel.md)
- [ASP.NET Core Standards](./standards/ASP.Net Core.md)

## Standard Structure

Each standards file should define:

- Naming rules
- File and folder organization expectations
- Code style and formatting expectations
- Design and architecture guidance
- Testing expectations
- Common anti-patterns to avoid

## Maintenance Notes

- Update standards when we identify a repeated code review issue.
- Prefer adding examples for rules that are easy to misunderstand.
- Keep standards opinionated enough to be useful, but practical enough for real delivery work.
