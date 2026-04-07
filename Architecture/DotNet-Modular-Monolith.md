# .NET Modular Monolith

## Purpose

Define the default architecture guidance for a .NET modular monolith application.

## When To Use

- One deployable unit is preferred.
- The domain is large enough to require clear module boundaries.
- Teams want strong internal separation without distributed system overhead.
- The product may later split selective modules into services.

## Core Principles

- Ship as one application, design as many modules.
- Keep modules isolated by contracts, not by folder names alone.
- Prefer synchronous in-process collaboration until there is a clear reason to distribute.
- Make module ownership and boundaries obvious in code.

## Recommended Structure

- One solution with clearly separated module projects or module folders.
- Shared host or web application as the composition root.
- Each module owns its application logic, domain logic, persistence, and integration adapters where practical.
- Cross-module dependencies should flow through explicit interfaces, contracts, or events.

## Module Boundaries

- A module should expose a narrow public surface.
- Internal implementation details should stay hidden.
- Avoid direct database access across modules.
- Avoid referencing another module's internals just because the code is in the same process.

## Data and Integration

- Prefer per-module persistence boundaries even if the same database server is used.
- Use application services, contracts, or internal messaging for cross-module workflows.
- Publish domain or integration events when loose coupling improves clarity.

## Testing

- Unit test module logic in isolation.
- Integration test module boundaries and host wiring.
- Add architecture tests where practical to enforce dependency rules.

## Avoid

- Shared utility layers that become a back door around module boundaries.
- Cross-module table access without an explicit contract.
- A single application project that mixes every feature together.
