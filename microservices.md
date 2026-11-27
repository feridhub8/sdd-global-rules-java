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
- `<project>-infrastructure` holds the Docker setup of infrastructure tools and nothing else, except tests for that setup: a `tests/` folder whose tests run as a container with docker compose.
- `<project>-specs` holds OpenSpec for all repos (see [workflow.md](workflow.md)).

## Infrastructure

- One folder per tool, containing only `docker-compose.yml`, `.env.example`, and config files the tool needs.
- A root `docker-compose.yml` lists every tool under `include:`, so all tools start and stop with docker compose.
- When I ask to add a tool, add only its Docker setup and include it in the root `docker-compose.yml`.
- No OS-specific scripts. Everything runs with docker compose commands, which work the same on every OS. Exception: scripts that run inside a container (for example a database init script) are allowed.
- Image tags are pinned to an exact version, never `latest`.

## Docker

- Every compose file sets `name: <project>`, so all compose files of a project form one Compose project.
- Compose files set no `container_name`. Compose names containers `<project>-<service>-<n>`, so a service can run several replicas.
- Every container joins the shared external network `<project>_network`.
- Before running Docker commands, the assistant checks that `<project>_network` exists and creates it when it is missing. The repo's `README.md` states that the network is required on every machine that runs the containers and gives `docker network create <project>_network`.

## Environments

- When development and production share one server or tool instance, development resources on it end with `Dev`: database names, and per-environment resources inside a shared tool instance, such as identity provider realms. Production names have no suffix.

## Boundaries

- A service never imports another service's code. Services communicate only through the method chosen for the project.
- Start small: build the minimum working set of services first, add the rest one proposal at a time.
