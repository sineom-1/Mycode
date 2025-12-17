---
name: coding-patterns
description: 跨语言的通用编码与设计模式（错误处理、边界划分、依赖管理、可测试性、性能与安全）
---

本 skill 提供与语言/框架无关的通用编码要点。目标是：更少的复杂度、更清晰的边界、更可测试的实现。

## 核心原则

- KISS：简单优于聪明
- YAGNI：只做当前明确需要的
- DRY：消除重复，但避免“为了抽象而抽象”
- SOLID：单一职责、依赖抽象、接口隔离

## 常用模式（通用）

### 1) 边界与核心分离

- 边界层负责：输入校验、鉴权/授权、参数解析、错误映射、日志埋点
- 核心逻辑负责：业务规则与可测试的纯逻辑

### 2) 错误处理与错误模型

- 不吞错；错误信息要带上下文（做什么失败、输入是什么、影响是什么）
- 对外错误要稳定：统一错误码/异常类型/响应结构

伪代码示例：

```text
function handler(input):
  validated = validate(input) or return error(BAD_REQUEST, details)
  result = service(validated) catch err:
    if isNotFound(err): return error(NOT_FOUND)
    if isConflict(err): return error(CONFLICT)
    log(err, context)
    return error(INTERNAL)
  return ok(result)
```

### 3) 依赖管理

- 依赖通过参数注入（构造函数/容器）而不是全局变量
- 依赖接口化，便于替换与测试

### 4) 数据与一致性

- 明确字段可空性与默认值；避免“靠约定”传递不变量
- 幂等与重试：外部调用要考虑超时、重试、重复请求

### 5) 性能与资源

- 先度量后优化；避免过早优化
- 注意资源释放（连接/文件/锁/订阅），避免无界队列与缓存

### 6) 安全基线

- 最小权限原则（鉴权、授权、数据访问）
- 输入校验与编码（防注入/越权/敏感信息泄露）
- 机密信息不入日志、不进仓库

