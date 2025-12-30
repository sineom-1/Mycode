# 未名配置（v1.1.0）

本仓库用于维护一套通用的「Commands + Agents + Skills」协作配置，面向日常开发中的探索、规划、实现、质检与文档整理。

## 入口规范

- 当前生效规范：`CLAUDE.md`

## 目录结构

- `commands/`：可复用的命令入口（如 `/dev`、`/explore`、`/plan`、`/code`、`/check`、`/doc`）
- `agents/`：子代理定义与使用指南（见 `agents/README.md`）
- `skills/`：可复用知识库（被 agents 引用），包含：
  - `skills/codebase-retrieval/`：代码库语义检索规范（基于 Auggie MCP）
  - `skills/coding-patterns/`：通用编码模式
  - `skills/frontend-design/`：前端设计与工程模式（视觉/组件/状态/数据/A11y/性能）
  - `skills/collaborating-with-codex/`、`skills/collaborating-with-gemini/`：Codex/Gemini CLI Bridge 调用规范（skills 模式）

## 推荐使用方式（最小闭环）

1. 先读 `CLAUDE.md`，确认本次需求的验收标准与边界。
2. 需要理解现状：用 `/explore`（入口定位、调用链、关键文件）。
3. 需要方案与拆解：用 `/plan`（多方案对比→推荐→步骤）。
4. 进入实现：用 `/code`（最小改动、可验证）。
5. 交付前质检：用 `/check`（高信号问题 + 回归建议）。
6. 需要补文档：用 `/doc`。

中大型需求建议直接使用 `/dev` 走完整 feature-dev 流程。

## 约定

- 对用户沟通使用简体中文（工具/命令/标识符保持原文）。
- 新增/修改文件统一为 UTF-8（无 BOM）。
