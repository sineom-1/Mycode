---
name: codebase-retrieval
description: 代码库语义检索规范（基于 Auggie MCP）
---

使用 Auggie MCP 进行语义化代码检索的统一规范。

## 工具

`mcp__auggie-context__codebase-retrieval`

## 适用场景

- 定位入口点（API、路由、命令、事件处理）
- 追踪调用链与数据流
- 理解架构模式与设计决策
- 探索模块边界与依赖关系
- 查找相似实现作为参考

## 查询方式

使用自然语言描述，支持 Where / What / How 类型查询：

```text
Where is the authentication handler?
What tests exist for the payment module?
How does the routing system work?
How is error handling implemented in the API layer?
```

## 检索原则

1. **禁止假设**：不基于猜测回答，必须有代码证据
2. **完整性优先**：获取类、函数、变量的完整定义与签名
3. **递归检索**：上下文不足时，触发追加查询直至信息完整
4. **先检索后行动**：在生成建议或代码前，必须先完成检索

## 与其他工具的分工

| 场景 | 推荐工具 |
|------|----------|
| 语义理解、架构探索、入口定位 | `codebase-retrieval` |
| 精确匹配标识符、查找所有引用 | `Grep` |
| 已知文件路径、查看特定内容 | `Read` |
| 文件名模式匹配 | `Glob` |
