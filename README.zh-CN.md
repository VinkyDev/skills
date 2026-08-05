# Vinky Skills

[English](README.md) | 简体中文

用于编写简洁、优雅、模块化且类型安全代码的 Agent 指令。

仓库提供两个版本，请根据项目所处阶段和兼容性要求选择合适的版本。

## 版本选择

### `writing-elegant-code`

适用于生产项目和即将进入生产环境的项目。

该版本在保护已确认的外部契约、生产数据和发布安全的前提下，将代码收敛到最简洁、持久的设计。只有在生产运行确实需要时才保留兼容逻辑或迁移，并要求这些逻辑与新核心设计隔离，同时具备明确的移除条件。

适合以下场景：

- 已上线或即将上线的应用；
- 公开 API 或已有外部调用方的 API；
- 生产数据持久化和 Schema 演进；
- 需要分阶段发布或可回滚发布的改动；
- 常规功能开发、重构、代码评审和依赖选择。

对应文件：

- Skill：[`skills/writing-elegant-code/SKILL.md`](skills/writing-elegant-code/SKILL.md)
- AGENTS.md 模板：[`docs/writing-elegant-code/AGENTS.md`](docs/writing-elegant-code/AGENTS.md)

### `writing-elegant-code-development`

适用于仍在研发阶段、可以接受破坏性变更的项目。

该版本要求移除向后兼容和过时路径，直接替换旧接口，同步更新仓库内所有调用方，不保留适配器、fallback、废弃别名、临时 feature flag 或迁移层。

适合以下场景：

- 尚未进入生产环境的项目；
- 原型和未发布系统；
- 内部研发分支；
- 尚未发布的 API、Schema 和数据模型；
- 整个仓库可以一次性切换到最终设计的重构。

如果已有部署中的调用方、生产数据、公开契约，或改动需要分阶段发布，请不要选择此版本，应使用 `writing-elegant-code`。

对应文件：

- Skill：[`skills/writing-elegant-code-development/SKILL.md`](skills/writing-elegant-code-development/SKILL.md)
- AGENTS.md 模板：[`docs/writing-elegant-code-development/AGENTS.md`](docs/writing-elegant-code-development/AGENTS.md)

## 安装方式

可以选择以下任一种方式安装。

### 方式一：作为 Skill 安装

运行 Skills 安装命令，并选择适合当前项目的版本：

```bash
npx skills@latest add VinkyDev/skills
```

这种方式会将指令安装为可复用的 Agent Skill，需要时可以调用对应 Skill。

### 方式二：作为项目指令安装

将所选版本的模板复制到目标项目根目录的 `AGENTS.md`。

生产项目或即将进入生产环境的项目：

```bash
cp docs/writing-elegant-code/AGENTS.md /path/to/your-project/AGENTS.md
```

仍在研发阶段且可以接受破坏性变更的项目：

```bash
cp docs/writing-elegant-code-development/AGENTS.md /path/to/your-project/AGENTS.md
```

如果目标项目已经存在 `AGENTS.md`，请将所选模板合并到现有文件中，不要覆盖项目原有的专属指令。采用这种方式后，Agent 在该项目中工作时会自动应用这些规则。

## 共同原则

两个版本都会要求 Agent：

- 在正确的抽象层解决根因；
- 从最小的端到端可用改动开始，以完整层次逐步扩展；
- 避免没有当前需求依据的抽象、配置和间接层；
- 保持组件模块化和关注点分离；
- 注释只解释“为什么”；
- 保持精确类型，TypeScript 中不使用 `any`；
- 新增依赖或自行实现通用能力前，先检查现有依赖、文档和类型；
- 选择持久的架构设计，不采用计划稍后替换的临时方案；
- 完成前运行相关类型检查、lint 和测试。
