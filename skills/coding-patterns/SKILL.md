---
name: coding-patterns
description: 跨语言的通用编码模式（边界划分、错误处理、依赖管理、数据一致性、性能与安全）
---

语言/框架无关的编码模式参考。聚焦：何时用、怎么用、常见错误。

## 1) 边界与核心分离

**适用**：API 入口、Controller、Gateway、CLI 命令处理

| 边界层 | 核心层 |
|--------|--------|
| 输入校验、鉴权、参数解析 | 业务规则、纯逻辑 |
| 错误映射、日志埋点 | 无副作用、可测试 |

**反模式**：在核心层直接返回 HTTP 状态码、直接写日志、直接访问 request 对象

## 2) 错误处理

**原则**：不吞错、带上下文、对外稳定

```text
handler(input):
  validated = validate(input) or return error(BAD_REQUEST, details)
  result = service(validated) catch err:
    if isNotFound(err): return NOT_FOUND
    if isConflict(err): return CONFLICT
    log(err, {action, input, user})  // 内部日志带上下文
    return INTERNAL                   // 对外错误结构稳定
  return ok(result)
```

**反模式**：`catch(e) { return null }`、错误信息只有 "failed"、内部异常直接暴露给用户

## 3) 依赖管理

**原则**：注入优于全局、接口优于实现

```text
// Good: 依赖注入
class OrderService(paymentGateway, inventory):
  ...

// Bad: 全局依赖
class OrderService:
  gateway = GlobalPaymentGateway.instance()
```

**反模式**：单例滥用、测试时需要 mock 全局状态、循环依赖

## 4) 数据一致性

**原则**：显式可空性、幂等设计、重试安全

- 字段定义明确 `required/optional`，不靠"约定"
- 外部调用带幂等键，支持安全重试
- 状态变更用乐观锁或版本号

**反模式**：`if (field != null)` 散落各处、重复提交导致重复扣款、并发更新丢失

## 5) 性能与资源

**原则**：先度量后优化、资源必释放

- 优化前先有 baseline 数据
- 连接/文件/锁/订阅 必须在 finally/defer/using 中释放
- 避免无界队列、无界缓存

**反模式**：凭直觉优化、连接泄漏、OOM 后才发现缓存无上限

## 6) 安全基线

**原则**：最小权限、输入不可信、机密不落盘

- 鉴权：验证身份；授权：验证权限；数据访问：验证所有权
- 输入校验 + 输出编码（防 SQL/XSS/命令注入）
- 机密不入日志、不进仓库、不硬编码

**反模式**：`isAdmin` 只在前端检查、日志打印完整请求体含密码、API Key 写在代码里
