# 功能承接与来源追溯

审计日期：2026-10-12。以下记录旧产品的需求出处、代码版本与验证状态。

## 来源优先级

1. 本次产品讨论的明确决定：MC Harness Bridge 品牌与六仓库拆分；面向外部 harness；玩家可继续游玩；丰富现场上下文；`agent-hooks` 接入无人值守 Agent；当前没有世界 merge/promotion。
2. 旧产品的明确需求、未闭环问题与实现所提供的行为证据。
3. 旧方案、试验分支和便利流程，作为候选设计输入。

旧本地产品重写合同也参与审计，但未提交内容不是公开基线。本稿将需承接的行为展开为稳定需求 ID；方案冲突以本次边界为准，具体差异见下文。

## 审计的代码版本

| 来源 | 审计 commit | 用途 |
| --- | --- | --- |
| [mc-agent](https://github.com/guajun/mc-agent/tree/f8c9f64c62da3ee72b8aa1e754935b6ccfa80ced) | `f8c9f64c62da3ee72b8aa1e754935b6ccfa80ced` | 产品需求、使用入口与跨仓库议题 |
| [mc-agent-bridge](https://github.com/guajun/mc-agent-bridge/tree/0ff0981b94786bd15f44382e20191c7a6a49fac5) | `0ff0981b94786bd15f44382e20191c7a6a49fac5` | Go CLI/daemon、协议命令、事件与 Webhook |
| [mc-agent-interface-mod](https://github.com/guajun/mc-agent-interface-mod/tree/cfe2c34bd8139a74a85ab9c7c6fe2ef0696ff8ef) | `cfe2c34bd8139a74a85ab9c7c6fe2ef0696ff8ef` | 游戏权威数据、同端口控制、实体导出与客户端功能 |
| [mc-agent-loop](https://github.com/guajun/mc-agent-loop/tree/a1b8bc52e1fc29c8e43f679522289c7fdf991f57) | `a1b8bc52e1fc29c8e43f679522289c7fdf991f57` | 旧 Agent loop 的职责与退役边界 |
| [jlink-cli](https://github.com/guajun/jlink-cli/tree/b2ca13f57474638e5e26352aafe068cc043be324) | `b2ca13f57474638e5e26352aafe068cc043be324` | Agent 使用调试原语、结构化结果与工具 Skill 的参考 |

## 模块来源

| 新需求 | 主要来源 | 承接判断 |
| --- | --- | --- |
| CTX-01…06 | Mod [#1](https://github.com/guajun/mc-agent-interface-mod/issues/1)、[#2](https://github.com/guajun/mc-agent-interface-mod/issues/2)，meta [#8](https://github.com/guajun/mc-agent/issues/8)，Mod [PR #13](https://github.com/guajun/mc-agent-interface-mod/pull/13) | 保留指定玩家视角、receipt、缓存来源与权威实体层级；不把服务端视线等同于完整客户端画面 |
| CON-01…08 | meta [#39](https://github.com/guajun/mc-agent/issues/39)、[#46](https://github.com/guajun/mc-agent/issues/46)、[#49](https://github.com/guajun/mc-agent/issues/49)，Mod [#8](https://github.com/guajun/mc-agent-interface-mod/issues/8) | 同游戏端口、独立多 daemon、实际实例隔离，覆盖专服/LAN/未发布 LAN 的本地访问 |
| OPS-01…08 | meta [#6](https://github.com/guajun/mc-agent/issues/6)、[#47](https://github.com/guajun/mc-agent/issues/47)、[#51](https://github.com/guajun/mc-agent/issues/51)，Mod [PR #12](https://github.com/guajun/mc-agent-interface-mod/pull/12) | 保留通用命令、真实反馈、未知写查询与最小协调；结果层次仍需完成新协议设计 |
| EVT-01…07 | meta [#4](https://github.com/guajun/mc-agent/issues/4)、[#5](https://github.com/guajun/mc-agent/issues/5)、[#50](https://github.com/guajun/mc-agent/issues/50) | 保留事件消费/Watch/时钟事实；细粒度事件仍是讨论项，不能用推测补齐真实链路 |
| SNP-01…09 | meta [#40](https://github.com/guajun/mc-agent/issues/40)、[#50](https://github.com/guajun/mc-agent/issues/50)、[#51](https://github.com/guajun/mc-agent/issues/51) | 核心目标是 Mod 拍摄 + Go 传输 + 外部 Agent 消费；旧实体导出不冒充完整世界快照 |
| CLT-01…06 | meta [#39](https://github.com/guajun/mc-agent/issues/39)，bridge 命令目录与 Mod 客户端实现 | 保留 GUI/聊天/录制/连接/世界/LAN 和单机本地路径，不能因服务端重写而遗忘 |
| HOK-01…06 | meta [#7](https://github.com/guajun/mc-agent/issues/7)，bridge [#2](https://github.com/guajun/mc-agent-bridge/issues/2)、[#7](https://github.com/guajun/mc-agent-bridge/issues/7) | 通用 Webhook 的旧实现是证据；Go 原生 Hermes 互操作是单独未闭环目标 |
| DST-01…08 | meta [#9](https://github.com/guajun/mc-agent/issues/9)、[#48](https://github.com/guajun/mc-agent/issues/48)、[#57](https://github.com/guajun/mc-agent/issues/57)、[#58](https://github.com/guajun/mc-agent/issues/58)、[#59](https://github.com/guajun/mc-agent/issues/59)，bridge [#11](https://github.com/guajun/mc-agent-bridge/issues/11)、[#12](https://github.com/guajun/mc-agent-bridge/issues/12)、[#13](https://github.com/guajun/mc-agent-bridge/issues/13)、[#21](https://github.com/guajun/mc-agent-bridge/issues/21) | Go 原生、CLI-only、安装与 Skill 分开；工具事实与实验方法分开；发行证据按实际组合建立 |

## 旧操作逐项去向

名称来自旧 Go protocol catalog。这里只追踪行为，不承诺保留旧命令拼写、旧 wire schema 或旧配置名。新命令及迁移映射在 CLI 设计定版后补充。

| 旧操作 | 新归属/需求 | 处理 |
| --- | --- | --- |
| `ping` | CON-05、DST-02 | 连通性和实例身份；不能证明任意能力可用 |
| `status` | CON-06、CON-08、DST-02 | daemon/连接/目标状态分别表达 |
| `capabilities` | OPS-08、CLT-05、DST-02 | 当前目标实际能力、权限与限制 |
| `state` | CTX-05、EVT-05 | 游戏/维度/运行状态与时钟事实 |
| `player` | CTX-01、CTX-02 | 明确指定玩家与实际观测来源 |
| `entities` | CTX-06 | 有界查询、NBT、order 与乘客层级 |
| `command` | OPS-01…04、OPS-08 | 保留通用执行，修正结果与未知状态契约 |
| `command_output` | OPS-01、OPS-02 | 保留真实反馈和关联；新 CLI 是否单独子命令待定 |
| `chat` | CLT-02 | 客户端聊天动作，不冒充服务端命令反馈 |
| `record_start` / `record_stop` | CLT-04 | 客户端录制原语与明确资源边界 |
| `wait` | EVT-05、EVT-06、OPS-07 | 说明等待的时钟、源状态、条件和取消 |
| `screen` | CLT-01 | 客户端界面状态；截图支持须单独声明 |
| `mark` | OPS-07、EVT-05 | 标记与事件/时间关联 |
| `connect` | CLT-03 | 明确客户端连接动作 |
| `world` | CLT-03 | 明确本地世界相关动作；不隐式打开/替换世界 |
| `lan` | CLT-03、CLT-06 | LAN 管理保留，同时保留无需发布 LAN 的本地访问 |
| `events` | EVT-01…04、EVT-06 | 分页/follow、游标、过滤、gap 与背压 |
| `context` | CTX-01…05 | 玩家 receipt、缓存来源和无玩家时的权威上下文 |
| `save` | SNP-01…04 | 旧保存/世界元数据不是新完整快照；保存是否属内部步骤需审计 |
| `snapshot` | CTX-06、SNP-01…04 | 旧实体导出单独标识；新增世界拍摄契约另立版本 |
| `snapshots` | SNP-02、SNP-05、SNP-08 | 产物清单、范围、状态与保留期；旧数据兼容待定 |
| `fork` | SNP-05、SNP-06、SNP-09 | 实验实例创建由外部 Agent/工具完成；核心提供可消费材料 |
| `restore` | SNP-09、DST-08 | 源服世界恢复不纳入当前核心；旧便利行为需明确迁移说明 |
| `verify` / `order` | CTX-06、EVT-05、SNP-09 | 捕获与读回事实保留，实验比对方法由外部 Agent 承担 |
| `request_status` | OPS-03、OPS-04 | 未知写查询，去重/保留窗口与重启边界 |
| `exclusive_acquire` / `exclusive_renew` / `exclusive_release` / `exclusive_status` | OPS-05、OPS-06 | 协调能力与事实查询保留；具体租约接口须按冲突矩阵设计 |
| `stop` | CON-06、CON-08 | 停止 daemon 不等于关闭游戏或解冻世界 |

## 来源状态与设计差异

- meta #40 的早期方案曾包含 Go 管理实验实例。本次职责已收敛：游戏侧拍摄、Go 控制/传输、外部 Agent 管理实验实例。需要实验的能力仍保留在需求中，运行编排归属改变。
- 旧 LAN 远程链路的验证拓扑和环境见 meta #49 与相关记录。
- 旧实体导出覆盖 NBT/order/passenger；世界快照另需审计磁盘世界、内存、随机数、调度队列和模组私有状态。
- 通用签名 Webhook 已有旧实现；Hermes 原生 Go V2 接入仍需实际接收、触发、调用工具和回复的完整证据。
- meta [PR #54](https://github.com/guajun/mc-agent/pull/54)、[PR #56](https://github.com/guajun/mc-agent/pull/56)，bridge [PR #19](https://github.com/guajun/mc-agent-bridge/pull/19) 中的审计/方法方案列为候选输入。
- 旧产品的合并、游戏测试、发行与消费记录分别追踪；消费验证需求见 meta #58。

## 迁移规则

需求变更或取消在 [decisions](decisions.md) 记录理由、替代路径与用户影响。旧仓库归档随新实现验收、迁移和发行单独规划。
