---
description: 代码探索（入口定位、调用链追踪、架构梳理）
argument-hint: What to explore
---

# 代码探索

调用 `explorer`，在不做假设的前提下快速理解指定功能/模块/问题的实现。

## 使用示例

```
/explore 用户登录流程
/explore 支付回调处理逻辑
/explore 某个接口为什么返回 500
/explore 前端某页面的数据来源
```

## 输出期望

- 入口与触发点（`file:line`）
- 执行流程（步骤化）
- 关键组件与职责
- 依赖与副作用
- 必读文件清单（最少但足够）

---

**探索目标**: $ARGUMENTS

