---
name: writing-elegant-code-development
description: Write and refactor simple, final, modular, type-safe code for projects still under active development where breaking changes are acceptable. Use when implementing or refactoring pre-production systems, prototypes, internal development branches, or unreleased APIs and schemas; remove backward compatibility, obsolete paths, fallbacks, and migrations instead of preserving them.
---

# Writing Elegant Code for Development

Move directly to the final design. Assume breaking changes are acceptable and remove every obsolete state rather than carrying it forward.

Do not use this skill when deployed consumers, persisted production data, public contracts, or staged rollouts require compatibility. Use `writing-elegant-code` instead.

## Working method

- Fix the root cause at the correct abstraction instead of adding a local patch.
- Start with the smallest end-to-end implementation that works, then add only capabilities required now.
- Complete each layer before adding the next; never replace a working system with unfinished complexity.
- Keep components modular, responsibilities focused, and concerns clearly separated.
- Finish the change across every abstraction it touches while leaving unrelated areas intact.
- Make architectural decisions for the long term. Do not introduce a stopgap intended to be replaced later.

## Design

- Choose the fewest concepts, paths, configuration options, and extension points that fully satisfy current requirements.
- Avoid speculative abstractions, indirection, and flexibility without a concrete use case.
- Do not preserve backward compatibility.
- Remove obsolete APIs, schemas, implementations, configuration, call sites, tests, and documentation in the same change.
- Replace old paths outright. Do not add adapters, compatibility branches, deprecated aliases, dual reads or writes, fallbacks, feature flags, or migration layers.
- Update all in-repository consumers to the final interface immediately.
- Keep one canonical representation and one normal execution path.

## Comments

- Prefer focused decomposition and precise names that make the code self-explanatory.
- Comment only decisions the code cannot express, explaining why: external constraints, counterintuitive behavior, invariants, or significant tradeoffs.
- Remove comments that restate what the code does, narrate an obvious flow, or have become stale.

## Types and boundaries

- Carry precise types through input boundaries, internal flows, and output boundaries.
- Validate untrusted data at the boundary before use.
- Never write explicit or implicit `any` in TypeScript. Use `unknown`, then narrow it with a type guard or schema.
- Use type assertions and non-null assertions only when a runtime check or explicit invariant proves them safe.
- Model invalid states out of the core design where practical instead of repeatedly checking them downstream.

## Libraries

- Inspect the project's dependencies, documentation, and types before implementing common functionality or adding a package.
- Prefer an existing modern dependency when it already provides the capability cleanly.
- Otherwise prefer a mature, actively maintained, widely adopted library when it reduces total complexity or improves reliability.
- When adding a library, use the latest stable version compatible with the project's runtime, toolchain, and peer dependencies, and follow its current documentation.
- Avoid duplicate dependencies for the same capability. Implement a few lines of clear domain logic directly when that is smaller than another dependency.

## Completion gate

Before finishing, verify every modified file and affected path:

- The implementation solves the root cause and works end to end.
- Every new concept and logic path serves a current requirement.
- The old implementation and all obsolete paths are gone.
- No adapters, compatibility branches, deprecated aliases, fallbacks, temporary flags, or migrations remain.
- Every in-repository consumer, test, fixture, and document uses the final design.
- Every comment passes the why test.
- TypeScript contains no `any`, and every `unknown` is narrowed before use.
- Existing dependencies were checked before adding or reimplementing functionality.
- Relevant type checks, lint checks, and tests pass.
