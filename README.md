# Vinky Skills

English | [简体中文](README.zh-CN.md)

Agent instructions for writing simple, elegant, modular, and type-safe code.

Two variants are provided. Choose the one that matches the lifecycle and compatibility requirements of your project.

## Variants

### `writing-elegant-code`

For production systems and production-bound projects.

This variant converges code toward the simplest durable design while protecting verified external contracts, persisted production data, and rollout safety. It retains compatibility or migrations only when operationally required, keeps them outside the new core design, and requires an explicit removal condition.

Choose it for:

- live or production-bound applications;
- public or externally consumed APIs;
- persisted production data and schema evolution;
- changes that require staged or reversible rollout;
- general implementation, refactoring, review, and dependency selection.

Files:

- Skill: [`skills/writing-elegant-code/SKILL.md`](skills/writing-elegant-code/SKILL.md)
- AGENTS.md template: [`docs/writing-elegant-code/AGENTS.md`](docs/writing-elegant-code/AGENTS.md)

### `writing-elegant-code-development`

For projects still under active development where breaking changes are acceptable.

This variant removes backward compatibility and obsolete paths, replaces old interfaces outright, updates every in-repository consumer, and leaves no adapters, fallbacks, deprecated aliases, temporary feature flags, or migration layers behind.

Choose it for:

- pre-production projects;
- prototypes and unreleased systems;
- internal development branches;
- unreleased APIs, schemas, and data models;
- refactors where the repository can move atomically to the final design.

Do not choose this variant when deployed consumers, persisted production data, public contracts, or staged rollouts require compatibility. Choose `writing-elegant-code` instead.

Files:

- Skill: [`skills/writing-elegant-code-development/SKILL.md`](skills/writing-elegant-code-development/SKILL.md)
- AGENTS.md template: [`docs/writing-elegant-code-development/AGENTS.md`](docs/writing-elegant-code-development/AGENTS.md)

## Installation

Choose one of the following installation methods.

### Option 1: Install as a Skill

Run the Skills installer and select the variant appropriate for your project:

```bash
npx skills@latest add VinkyDev/skills
```

This method keeps the instructions as a reusable agent skill that can be invoked when needed.

### Option 2: Install as project instructions

Copy the selected template to `AGENTS.md` at the root of your project.

For production and production-bound projects:

```bash
cp docs/writing-elegant-code/AGENTS.md /path/to/your-project/AGENTS.md
```

For projects still under active development where breaking changes are acceptable:

```bash
cp docs/writing-elegant-code-development/AGENTS.md /path/to/your-project/AGENTS.md
```

If the target project already has an `AGENTS.md`, merge the selected template into it instead of overwriting existing project-specific instructions. This method applies the rules automatically whenever an agent works in that project.

## Shared principles

Both variants require agents to:

- solve root causes at the correct abstraction;
- build the smallest working end-to-end change and grow it in complete layers;
- avoid speculative abstraction, configuration, and indirection;
- keep components modular and concerns separated;
- write comments only to explain why;
- maintain precise types and never use TypeScript `any`;
- inspect existing dependencies, documentation, and types before adding packages or reimplementing common functionality;
- prefer durable architecture over temporary solutions;
- run relevant type checks, lint checks, and tests before finishing.
