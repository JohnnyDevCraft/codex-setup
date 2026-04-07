# .NET Micro Services

## Purpose

Define the default architecture guidance for a .NET microservices system.

## When To Use

- The domain can be split into independently deployable bounded contexts.
- Teams need high autonomy across services.
- Independent scaling, release cadence, and ownership are required.
- The organization is prepared for distributed system complexity.

## Core Principles

- Service boundaries follow business capabilities, not technical layers.
- Each microservice owns its own data and lifecycle.
- Operational concerns are part of the design, not an afterthought.
- Prefer autonomy over convenience when choosing boundaries.

## Recommended Structure

- One service per bounded context or narrowly scoped business capability.
- Separate deployable apps for APIs, workers, and event processors as needed.
- Shared platform components for observability, security, and delivery pipelines.

## Service Design

- Keep services small enough to own well, but large enough to be meaningful.
- Expose explicit API and event contracts.
- Avoid shared domain models across services.
- Keep synchronous dependencies few and intentional.

## Data and Integration

- Use database-per-service.
- Prefer event-driven communication for cross-service propagation where eventual consistency is acceptable.
- Handle duplicates, retries, and out-of-order events safely.
- Model sagas or process managers when workflows cross service boundaries.

## Testing

- Unit test domain and application logic.
- Contract test APIs and event schemas.
- Integration test infrastructure and messaging flows.
- Run end-to-end tests only for a focused set of critical business flows.

## Avoid

- Splitting into microservices before stable domain boundaries exist.
- Shared persistence across services.
- Excessive platform abstraction that hides what each service actually does.
