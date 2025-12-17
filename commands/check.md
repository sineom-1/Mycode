---
description: 质量检查（代码审查、测试策略、问题诊断）
argument-hint: Review / test / debug request
---

# 质量检查

调用 `guardian` 进行审查、测试建议或问题诊断。默认不改业务逻辑，重点输出高优先级、可执行的结论。

## 使用示例

```
/check review 这次改动是否有兼容性风险
/check test 为关键流程补齐测试策略
/check debug 线上出现间歇性超时，如何定位
```

## 输出期望

- 严重/重要/建议分级的问题清单（含 `file:line`）
- 建议的测试与回归范围
- 诊断思路与最小复现（如适用）

---

**检查任务**: $ARGUMENTS

