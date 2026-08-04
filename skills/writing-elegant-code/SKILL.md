---
name: writing-elegant-code
description: Converges code toward a simple, elegant, type-safe final design. Use when implementing or refactoring code, reviewing code quality, or selecting libraries.
---

# Writing Elegant Code

Use convergence as the standard: move directly to the final design without leaving temporary states, migration layers, or patches in the codebase.

## Comments

- Prefer focused decomposition and precise names that make the code self-explanatory.
- Comment only decisions the code cannot express, explaining why: external constraints, counterintuitive behavior, or significant tradeoffs.
- Remove comments that restate what the code does, narrate an obvious flow, or have become stale.

## Design

- Fix the root cause at the correct abstraction, converging on the fewest concepts and the single path needed by current requirements.
- Remove superseded logic in the same change; every intermediate layer, branch, special case, and extension point must serve a current requirement.
- Keep a compatibility path only for an explicit requirement or verified external contract, with a clear boundary from the normal path.
- Complete the change within every abstraction it touches while leaving unrelated areas intact.

## Types

- Carry precise types through input boundaries, internal flows, and output boundaries; validate untrusted data at the boundary before use.
- Never write explicit or implicit `any` in TypeScript. Use `unknown` for unknown values, then narrow with a type guard or schema before passing them onward.
- Use type assertions and non-null assertions only when a runtime check or explicit invariant proves them safe.

## Libraries

- Before implementing an established practice, inspect the project's existing dependencies and ecosystem options; prefer a mature, actively maintained, widely adopted library.
- When adding a library, use the latest stable version compatible with the project's runtime, toolchain, and peer dependencies, and follow its current documentation.
- Prefer a modern library already present in the project and avoid duplicate dependencies for the same capability; implement a few lines of clear domain logic directly.

## Completion gate

Before finishing, check every modified file:

- Every comment passes the why test.
- Every new concept and logic path serves a current requirement, and every superseded implementation is gone.
- TypeScript contains no `any`, and every `unknown` is narrowed before use.
- Mature capabilities are delegated to an appropriate library, or the custom implementation is demonstrably smaller and clearer.
- Relevant type checks, lint checks, and tests pass.
