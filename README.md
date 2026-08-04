# Vinky Skills

Agent skills for writing simple, elegant, type-safe code.

面向简洁、优雅、类型安全代码的 Agent Skills。

## Skills

### `writing-elegant-code`

Converges code toward a final design that is concise, elegant, and type-safe. Use when implementing or refactoring code, reviewing code quality, or selecting libraries.

将代码收敛到简洁、优雅且类型安全的最终设计。适用于编写/重构代码、评审代码质量、选择依赖库。

It covers four areas / 覆盖四个方向：

- **Comments / 注释** — Prefer clear naming and decomposition; comment only the why, never the what.  
  优先用拆分与命名自解释；只写解释「为什么」的必要注释，不重复说明「做什么」。
- **Design / 设计** — Converge in one thorough change; avoid intermediate layers, compatibility branches, and patch-style fixes.  
  一次彻底改到位；少写中间/过度逻辑、兼容性逻辑与补丁式修改。
- **Types / 类型** — Keep TypeScript type-safe; never use `any`, prefer `unknown` and narrow before use.  
  尽可能保证类型安全；TypeScript 始终不写 `any`，必要时用 `unknown` 并在使用前缩窄。
- **Libraries / 库** — Prefer mature, modern libraries at their latest compatible versions over reinventing the wheel.  
  成熟实践优先用库实现；优先现代库及其最新兼容版本，避免重复造轮子。

### `writing-elegant-code-cn`

Chinese version of the same skill. Invoke by name when you want Chinese instructions.

同 skill 的中文版本。

## Install / 安装

```bash
npx skills@latest add VinkyDev/skills
```
