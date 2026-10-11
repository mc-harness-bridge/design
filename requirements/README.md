# 模块化需求索引

状态：首版需求基线；所有新产品实现状态均为未验收。

需求 ID 用于跨仓库追踪，不与 issue 号绑定。MUST 表示本轮必须承接的目标；TBD 表示目标已有依据而实现语义尚需设计；DISCUSSION 表示保留待讨论需求，不提前扩张为正式能力。历史实现存在不等于新实现完成。

## 模块与验收关联

| 模块 | ID | Owner | 需求文件 | 验收组 |
| --- | --- | --- | --- | --- |
| 玩家现场 | CTX-01…CTX-06 | mod + cli | [context](context.md) | AC-CONTEXT |
| 连接与部署 | CON-01…CON-08 | mod + cli | [connection](connection.md) | AC-CONNECTION |
| 操作与结果 | OPS-01…OPS-08 | mod + cli | [operations](operations.md) | AC-OPERATIONS |
| 事件与时间 | EVT-01…EVT-07 | mod + cli | [events](events.md) | AC-EVENTS |
| 快照与传输 | SNP-01…SNP-09 | mod + cli | [snapshots](snapshots.md) | AC-SNAPSHOT |
| 客户端与本地访问 | CLT-01…CLT-06 | mod + cli | [client](client.md) | AC-CLIENT |
| Agent hooks | HOK-01…HOK-06 | cli + agent-hooks | [agent-hooks](agent-hooks.md) | AC-HOOKS |
| CLI、安装与 Skill | DST-01…DST-08 | cli + mod + 主仓库 | [distribution](distribution.md) | AC-DISTRIBUTION |

详细需求共 58 项。每项包含行为、限制和可复核验收；[traceability](../traceability.md) 记录来源与旧功能映射。[验收矩阵](../acceptance.md) 规定证据类型，不把测试数量当作需求覆盖。

## 横跨模块的约束

- 所有查询和产物标明 source instance、run、vantage、dimension 或适用范围。
- 所有缓存、队列、采样、传输和保留策略有边界；具体数值在预算实测后固定。
- 权限来自认证会话，与被观察玩家和聊天 sender 分离。
- capability/schema 反映当前目标实际支持，未实现或不可用能力有原因。
- 错误、空结果、缺失、过期、不支持、结果未知和部分完成分别表达。
- 不隐式加入玩家身体、加载区块、冻结/解冻、服务器进程或实验编排。

## 变更规则

增加或取消需求必须记录来源与原因；需求编号不重复使用。旧实现的删除不能自动取消需求。字段与接口的具体变化由设计和实现 PR 共同追踪，产品能力只有在对应证据存在后才可标记为已交付。
