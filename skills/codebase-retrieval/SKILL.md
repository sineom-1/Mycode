---
name: codebase-retrieval
description: 代码库语义检索规范（基于 Auggie MCP）
---

使用 Auggie MCP 进行语义化代码检索的统一规范。

## 工具使用

### 工具选择优先级（严格执行）

**代码探索和搜索的工具使用顺序（从高到低）：**

```
1. mcp__auggie-context__codebase-retrieval  ← 最高优先级，语义搜索首选
   ├─ 适用：代码库整体理解、架构分析、跨文件关系探索
   └─ 优势：实时索引、语义理解、多语言支持

2. Grep/Glob 工具                       ← 次优先级，精确匹配
   ├─ 适用：已知文件名/路径、精确字符串匹配
   └─ 优势：速度快、结果准确

3. Task(Explore) 子代理                 ← 最低优先级，最后的选择
   ├─ 适用：前两者都不适用的复杂探索场景
   └─ 劣势：消耗更多上下文、速度较慢
```

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
