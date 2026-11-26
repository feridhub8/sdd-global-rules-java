# Microservices

Applies to projects built as microservices on Spring Boot.

## Decided per project

Decide these with me for each project and record the decision in the project's `openspec/config.yaml`:

- Package layout inside a service.
- Database: one per service, shared, or mixed; and the database engine.
- Whether development and production databases share one server or run on separate servers.
- API gateway.
- Communication between services: synchronous protocol and/or message broker.
- Infrastructure tools.

## Repositories

- One GitHub repository per service.
- Each microservice is `<project>-ms-<name>`, with `<name>` in lowercase kebab-case. Never `<name>-service`.
- `<project>-api-gateway` is the single entry point for clients.
- `<project>-infrastructure` holds the Docker setup of infrastructure tools and nothing else.
- `<project>-specs` holds OpenSpec for all repos (see [workflow.md](workflow.md)).

## Boundaries

- A service never imports another service's code. Services communicate only through the method chosen for the project.
- Start small: build the minimum working set of services first, add the rest one proposal at a time.
