# Codex Guidance for FTGO Application

## Scope

This file applies to `/home/dev/ftgo-application`.

This repository is used as local code evidence for studying `Микросервисы. Паттерны разработки и рефакторинга` from the Obsidian vault.

## Default Mode for Book Tasks

- Default to read-only inspection when the task is about the book, listings, architecture examples, contracts, tests, or deployment examples.
- Do not refactor, modernize, reformat, upgrade dependencies, or change runtime behavior during book-analysis tasks.
- Do not commit or push unless the user explicitly requests it.
- Preserve unrelated user changes.

## Useful Search Targets

- Gradle modules: `settings.gradle`, root `build.gradle`, and module `build.gradle` files.
- Domain and service code: `ftgo-order-service`, `ftgo-kitchen-service`, `ftgo-delivery-service`, `ftgo-consumer-service`, `ftgo-restaurant-service`.
- API and contracts: `*-service-api`, `*-service-contracts`, Spring Cloud Contract files, messaging contracts.
- Query/read-model code: `ftgo-order-history-service`.
- External API examples: `ftgo-api-gateway`.
- Tests: unit, integration, component, and `ftgo-end-to-end-tests`.
- Deployment examples: `docker-compose.yml`, `docker-compose-api-gateway-graphql.yml`, Kubernetes manifests if present, and `ftgo-restaurant-service-aws-lambda`.

## Listing Verification Rules

- Search with `rg` for exact class, method, package, contract, and module names from the book.
- Treat code as matching a book listing only when the surrounding context supports the match.
- If code differs from the book, report the difference instead of rewriting it.
- If a listing is not found, say `not found in local FTGO repository`.

## Validation

For read-only mapping tasks, prefer:

```bash
rg -n "ClassOrMethodName" /home/dev/ftgo-application
git -C /home/dev/ftgo-application status --short
```

For any future code edits requested by the user, inspect the relevant Gradle module first and run the narrowest applicable test or build command before claiming completion.

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

When the user types `/graphify`, invoke the `skill` tool with `skill: "graphify"` before doing anything else.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- Dirty graphify-out/ files are expected after hooks or incremental updates; dirty graph files are not a reason to skip graphify. Only skip graphify if the task is about stale or incorrect graph output, or the user explicitly says not to use it.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).
