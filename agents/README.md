# Agents 使用指南（通用）

本目录提供一组**语言/框架无关**的 sub-agents，用于支持以官方 `feature-dev` 为主的协作开发流程（Discovery → Exploration → Clarifying Questions → Architecture → Implementation → Review → Summary）。`feature-dev/` 目录保留官方原始示例，供对照参考。

## Agent 列表

| Agent | 职责 | 工具权限（建议） | 引用 Skills |
|---|---|---|---|
| `explorer` | 代码检索、入口定位、调用链追踪、架构梳理 | 只读 | `project-standards` |
| `architect` | 需求澄清、方案设计、任务拆解、风险评估 | 只读 | `project-standards`, `coding-patterns`, `frontend-patterns` |
| `coder` | 功能实现、重构优化、缺陷修复、测试补齐 | 读写 | `project-standards`, `coding-patterns`, `frontend-patterns`, `templates` |
| `guardian` | 代码审查、测试策略、问题诊断、回归建议 | 读写（默认不改业务逻辑） | `project-standards`, `quality-patterns` |
| `doc-writer` | API/技术/使用文档、变更说明、必要注释 | 读写（仅文档范围） | `project-standards`, `templates` |

## Skills 知识库

Agents 通过 frontmatter 的 `skills` 字段引用共享知识库：

| Skill | 内容 |
|---|---|
| `project-standards` | 如何识别并遵循目标项目的约定（目录/命名/构建/测试/发布） |
| `coding-patterns` | 跨语言的通用编码与设计模式（错误处理/边界/依赖/安全/性能） |
| `frontend-patterns` | 框架无关的前端工程模式（组件/状态/数据获取/A11y/性能） |
| `quality-patterns` | 审查标准、测试策略、调试与问题诊断方法 |
| `templates` | 常用文档/接口/变更模板 |
| `codex-mcp` | Codex MCP 细则（工具参数、会话、原型 unified diff、Review） |
| `gemini-mcp` | Gemini MCP 细则（需求澄清、前端原型 unified diff、边界与会话） |
| `frontend-design` | 官方前端设计 skill（可选） |

## 使用原则（KISS）

- 主对话充当调度器：确定目标与验收标准，按需调用 agents 获取结果
- 先探索再规划：不理解现状不要直接设计；不清楚需求不要直接实现
- 结果要可执行：任何输出都要指向具体文件与可验证步骤
- 不做无关重构：优先最小变更、最大复用

## 对应 Commands

| Command | 主 Agent | 说明 |
|---|---|---|
| `/dev` | 多个 | 完整开发流程（对齐官方 feature-dev 阶段与约束） |
| `/explore` | `explorer` | 代码检索与架构理解 |
| `/plan` | `architect` | 方案设计与任务拆解 |
| `/code` | `coder` | 代码实现与重构 |
| `/check` | `guardian` | 审查/测试/诊断 |
| `/doc` | `doc-writer` | 文档编写与整理 |
