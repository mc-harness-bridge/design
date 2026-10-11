# Agent hooks 与无人值守接入

Owner：cli 生产投递；agent-hooks 接入契约与真实互操作。状态：MUST，接收方格式按实际版本核实。

| ID | 行为与限制 | 验收 |
| --- | --- | --- |
| HOK-01 | 可选、默认关闭的游戏事件 webhook；可选择事件类型/来源，body 保留源事件身份、context_id 和实际时点。交互式 CLI 不依赖它。 | 禁用时无投递；启用后目标事件到达，过滤正确；普通终端路径无需 Hermes/Gateway。 |
| HOK-02 | 支持明确的通用签名模式及原生 Hermes V2 接收方协议，签名、timestamp、body bytes 和 delivery ID 遵守各自契约。签名选项与默认策略明确。 | 固定版本的合法、错误、过期签名；精确字节样例；不能把仅换 header 当作协议兼容。 |
| HOK-03 | 稳定投递身份跨重试不变；有界队列、有限重试、失败/溢出统计，不承诺跨任意重启持久交付或 exactly-once。 | 接收已成功但响应丢失、5xx、超时、队列满、耗尽、重启；对声明去重的接收方验证窗口内只触发一次，其他接收方说明重复风险。 |
| HOK-04 | Hermes V2 适配在 Go 原生投递链路完成，不要求 Python 转签常驻进程；不安装或管理 Hermes。 | 新环境只有 Go + Mod 和用户已运行的 Hermes；无 shim 仍接受真实 secret-protected route。 |
| HOK-05 | 真实 Hermes 任务可读取事件现场、加载工具 Skill、执行至少一次 CLI 操作并把回复发向用户配置的目标。 | 保存 Hermes 版本/route 配置、触发记录、工具调用和正确回复目标；fake receiver 不替代实际任务。 |
| HOK-06 | agent-hooks 提供接收方契约、配置示例、fixtures、互操作测试和版本证据；不复制 Go 队列、创建会话引擎或第三项目服务。 | repo 内容和生产安装依赖可核对；接入版本锁定，更新有回归；配置不含真实 secret。 |

## 责任分界

Hermes/用户管理模型、终端和文件权限、Gateway、route、会话、触发词、回复目标与自身去重。Go 管理事件投递与接收方协议选择，Mod 不知道 harness 名。

报告任务被触发、HTTP 接受、工具调用成功和最终回复，是不同证据。产品不把一次 HTTP 2xx 当作 Agent 已完成工作。
