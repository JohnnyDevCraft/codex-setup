# C# Standards

## Purpose

Define default coding standards for C# code across services, applications, libraries, and tests.

## Baseline

This standard starts from Microsoft's published .NET and C# conventions, then adds team-level guidance where Microsoft leaves room for local choice.

### Microsoft Published Baseline

- `.NET coding conventions` on Microsoft Learn
- `Common C# code conventions` on Microsoft Learn
- `.editorconfig` conventions used in Microsoft-maintained .NET repositories

## Core Principles

- Follow standard .NET naming and layout conventions first.
- Write clear, readable code before clever code.
- Prefer explicit domain language over vague utility naming.
- Use composition and dependency injection instead of hidden global state.
- Keep code easy to scan in the same way Microsoft code samples and product repos are easy to scan.

## Naming

- Use `PascalCase` for classes, records, enums, interfaces, methods, properties, and public constants.
- Prefix interfaces with `I`.
- Use `camelCase` for local variables and method parameters.
- Use meaningful nouns for types and verbs for methods.
- Use meaningful names that describe intent, not implementation detail.
- Name async methods with the `Async` suffix.

## File Organization

- Keep one primary public type per file.
- Match file names to the primary type name.
- Use folder structure that communicates product area or feature area clearly.
- Group by feature or domain where practical, not only by technical layer.
- Keep tests in a separate test project mirroring the production structure.

## Style

- Use file-scoped namespaces unless a block-scoped namespace is required.
- Use four spaces for indentation.
- Open braces stay on their own line for type and member declarations.
- Keep `using` directives at the top of the file.
- Sort `System` namespaces first.
- Prefer constructor injection for dependencies.
- Prefer expression-bodied members only when they improve readability.
- Use `var` when the type is obvious from the right-hand side; otherwise prefer explicit types.
- Keep nullable reference types enabled.
- Avoid deeply nested conditionals; return early when possible.
- Prefer language keywords like `string`, `int`, and `bool` over framework type names in declarations where standard .NET style does the same.

## Layout

- Order file contents so the public surface is easy to find quickly.
- Keep related members together.
- Prefer shorter methods with one clear job.
- Extract private helper methods when a method starts mixing multiple concerns.
- Avoid regions unless they solve a real readability problem in an otherwise large, legacy file.

## Design Guidance

- Keep domain logic out of controllers and UI concerns.
- Use records for immutable value-focused data shapes where they fit naturally.
- Prefer small service abstractions over static helper classes.
- Validate inputs close to the application boundary.
- Keep side effects explicit and easy to trace.
- Prefer dependency inversion at boundaries instead of reaching into static infrastructure from domain code.
- Follow existing .NET framework patterns before inventing custom patterns.

## Error Handling

- Do not swallow exceptions.
- Throw specific exceptions when the caller can act on the distinction.
- Use guard clauses for invalid input.
- Log enough context to diagnose failures without leaking secrets.

## Testing

- Write unit tests for domain and application logic.
- Keep tests deterministic and isolated.
- Use descriptive test names that state behavior.
- Prefer testing observable behavior over implementation details.

## Avoid

- God classes and catch-all utility files.
- Hidden static state.
- Long methods with multiple responsibilities.
- Boolean parameter overloads that make call sites unclear.

## Notes

- When a repository already contains an `.editorconfig`, analyzer rules, or SDK-specific conventions, those repository rules take precedence over this document.
