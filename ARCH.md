# Architecture Catalog

This folder centralizes reusable architecture guidance across projects.

## How To Use These Architectures

- Identify the architecture used by the target project before making structural changes.
- Read the relevant architecture document in `./Architecture`.
- Apply both the project architecture guidance and the language/framework standards from [STD.md](./STD.md).
- When a project combines multiple architectures, load each applicable document.

## Architecture Index

### .NET

- [.NET Modular Monolith](./Architecture/DotNet-Modular-Monolith.md)
- [.NET Distributed App](./Architecture/DotNet-Distributed-App.md)
- [.NET Micro Services](./Architecture/DotNet-Micro-Services.md)
- [.NET N-Tier Monolith](./Architecture/DotNet-N-Tier-Monolith.md)

### PHP

- [PHP Laravel Modular Monolith](./Architecture/PHP-Laravel-Modular-Monolith.md)

### Frontend and Workspace

- [Angular FrontEnd](./Architecture/Angular-FrontEnd.md)
- [Nx Workspace](./Architecture/Nx-Workspace.md)
- [Ionic Angular](./Architecture/Ionic-Angular.md)
- [Electron Wrapped Angular](./Architecture/Electron-Wrapped-Angular.md)

### Apple

- [SwiftUI App](./Architecture/SwiftUI-App.md)

## Architecture Document Structure

Each architecture file should define:

- Purpose and scope
- When to use it
- Core principles
- Recommended project structure
- Dependency boundaries
- Data and integration patterns
- Testing expectations
- Common risks and anti-patterns

## Maintenance Notes

- Update these documents when we discover repeated architecture review issues.
- Keep architecture guidance practical and implementation-oriented.
- Prefer decisions that make module boundaries, ownership, and deployment concerns easier to understand.
