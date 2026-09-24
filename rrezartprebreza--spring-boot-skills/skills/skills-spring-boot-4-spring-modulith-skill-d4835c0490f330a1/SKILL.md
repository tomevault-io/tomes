---
name: spring-modulith
description: > Use when this capability is needed.
metadata:
  author: rrezartprebreza
---

# Spring Modulith

## Spring Boot 4 baseline

Use the Spring Modulith 2.x line matching the exact Boot 4 minor; do not import a Boot 3 Modulith 1.x BOM.

## Apply within the existing architecture

Inspect the application root package, module boundaries and current dependency graph.
Use direct subpackages as modules; keep their API at the module root and implementation in
internal subpackages. Expose a named interface only for an intentional shared API.
Use allowedDependencies when the architecture needs explicit dependency constraints.
Avoid creating a generic shared module that every feature depends on.

## Verify boundaries

Add spring-modulith-starter-test with test scope and run
ApplicationModules.of(Application.class).verify() in CI. It checks cycles and access to module
internals. Add ApplicationModuleTest for behavior confined to a module. A passing structure
check does not prove transactional or delivery correctness.

See [good module verification](examples/good-module-test.java) and
[bad cross-module dependency](examples/bad-module-dependency.java).

## Reliable events

Publish immutable event payloads containing IDs and necessary facts, not managed JPA entities.
Use ApplicationModuleListener for asynchronous transactional listeners when that timing fits.
For delivery that must survive a process crash, configure a persistent event publication
registry using the chosen JDBC/JPA starter and manage its schema through migrations.
An in-memory registry and a plain after-commit callback are not durable delivery.

Make handlers idempotent: a crash after the business effect but before recording completion
can cause redelivery. Define retry/republication and retention explicitly, and test failed
listeners and application restarts. For external brokers, use supported event externalization
with persistent publication tracking; do not promise end-to-end exactly-once processing.

## Gotchas

- Agent imports a repository from another module's internal package - call its public API or consume an event.
- Agent adds Modulith to a simple unrelated task - preserve the requested scope.
- Agent assumes ApplicationModuleListener alone guarantees durability - configure persistent publication tracking.
- Agent publishes an entity with lazy associations - publish an immutable event contract.
- Agent tests only the happy path - verify cycles, module access and event redelivery.

## Official sources

- [Module verification](https://docs.spring.io/spring-modulith/reference/verification.html)
- [Events and publication registry](https://docs.spring.io/spring-modulith/reference/events.html)
- [Compatibility](https://docs.spring.io/spring-modulith/reference/appendix.html)

---
> Source: [rrezartprebreza/spring-boot-skills](https://github.com/rrezartprebreza/spring-boot-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
