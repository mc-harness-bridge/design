# MC Harness Bridge — Design

MC Harness Bridge 连接正在运行的 Minecraft 与外部 AI Agent harness，让 Agent 从玩家的现场获取上下文、观察状态、执行明确操作并取得游戏快照，同时尽量不打断玩家游玩。

**文档状态：2026-10-12 首版设计草案。** 正文记录产品边界与继承需求；协议字段、目录结构和实现方案待定。当前处于设计阶段。

## 阅读顺序

1. [产品哲学](philosophy.md)：使用场景、不侵入原则与设计取舍。
2. [架构与模块边界](architecture.md)：两个运行组件、六个仓库、数据与控制流。
3. [模块化需求总表](requirements/README.md)：稳定需求 ID、责任方与验收索引。
4. [功能承接与来源](traceability.md)：旧功能去向与历史证据。
5. [决策与待定问题](decisions.md)：已确认边界、建议方案和实施前要解决的具体问题。
6. [实施顺序](roadmap.md) 与 [验收矩阵](acceptance.md)。

## 需求与设计

| 模块 | 详细需求 | 对应设计 |
| --- | --- | --- |
| 玩家现场与权威观测 | [context](requirements/context.md) | [上下文与实体数据](contracts/context-and-entities.md) |
| 连接、身份与多会话 | [connection](requirements/connection.md) | [控制通道](contracts/control.md) |
| 操作、结果与协调 | [operations](requirements/operations.md) | [请求与结果](contracts/requests.md) |
| Watch、事件与时钟 | [events](requirements/events.md) | [事件与时钟](contracts/events-and-time.md) |
| 世界快照与产物传输 | [snapshots](requirements/snapshots.md) | [快照与产物](contracts/snapshots.md) |
| 客户端与本地访问 | [client](requirements/client.md) | [架构部署矩阵](architecture.md#部署矩阵) |
| 无人值守 Agent 接入 | [agent-hooks](requirements/agent-hooks.md) | [Webhook 与 Hermes](contracts/agent-hooks.md) |
| CLI、安装、Skill 与发行 | [distribution](requirements/distribution.md) | [兼容性与交付](contracts/distribution.md) |

## 仓库体系

- [mc-harness-bridge](https://github.com/mc-harness-bridge/mc-harness-bridge)：产品入口、跨仓库需求与兼容组合。
- [cli](https://github.com/mc-harness-bridge/cli)：一个 Go CLI/daemon 二进制、安装发行、工具 Skill。
- [mod](https://github.com/mc-harness-bridge/mod)：Fabric Mod，游戏侧权威原语。
- [design](https://github.com/mc-harness-bridge/design)：产品需求、设计依据、决策记录。
- [convention](https://github.com/mc-harness-bridge/convention)：开发、Git、worktree、验证和交付约定。
- [agent-hooks](https://github.com/mc-harness-bridge/agent-hooks)：外部 harness 的事件接入契约、配置、样例和互操作验证。

Design 说明产品需要什么和为什么；convention 说明如何开发与协作。具体线协议及跨语言 fixture 在实现前确定唯一维护位置，避免两个仓库维护不同版本的真相。

历史 `guajun/mc-agent*` 仓库的需求与证据见 [来源追溯](traceability.md)。
