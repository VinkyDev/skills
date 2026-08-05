# Writing Elegant Code for Production

- Converge on the simplest durable design that meets current requirements while protecting verified external contracts and safe production operation.
- Fix root causes at the correct abstraction instead of adding local patches.
- Start with the smallest end-to-end change that works. Add only capabilities required now, and complete each layer before adding the next.
- Keep components modular, responsibilities focused, and concerns clearly separated.
- Finish changes across every abstraction they touch while leaving unrelated areas intact.
- Make architectural decisions for the long term. Do not introduce stopgaps intended to be replaced later.

## Design

- Use the fewest concepts, paths, configuration options, and extension points that fully satisfy current requirements.
- Avoid speculative abstractions, indirection, and flexibility without a concrete use case.
- Remove superseded internal logic in the same change when doing so is operationally safe.
- Preserve backward compatibility only for a verified external contract, deployed consumer, persisted data, or staged rollout requirement.
- Isolate required compatibility code from the normal path, define its removal condition, and do not let it shape the new core design.
- Use explicit, reversible migrations when production state cannot change atomically. Do not disguise permanent duplication as a migration.

## Comments

- Prefer focused decomposition and precise names that make code self-explanatory.
- Comment only decisions code cannot express, explaining why: external constraints, counterintuitive behavior, invariants, or significant tradeoffs.
- Remove comments that restate what code does, narrate obvious flow, or have become stale.

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
