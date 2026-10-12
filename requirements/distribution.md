# CLI、安装、Skill 与发行

Owner：cli；mod 兼容发行；主仓库汇总。状态：MUST，二进制名称和最终版本策略 TBD。

| ID | 行为与限制 | 验收 |
| --- | --- | --- |
| DST-01 | 一个 Go 二进制提供 CLI/daemon；常规游戏调用非交互、参数可发现、稳定结构化输出，stdout 与诊断分开。version/help 的文本与 JSON 入口明确。 | 干净环境没有 Python/Go 开发工具/MCP 也可调用；所有声明的输出路径符合文档和退出码。 |
| DST-02 | 提供目标配置、生命周期、doctor/status/capabilities/schema、调用和事件入口；离线工具目录与目标实际能力区分。 | 离线诊断、连接失败、版本不匹配、目标不支持及权限过滤；返回当前可用状态与原因。 |
| DST-03 | 用户级安装把二进制放入 PATH；校验、固定版本、升级、卸载与当前/新 shell 生效说明完整。平台按实际测试声明。 | Windows/Linux/macOS 的已声明组合逐项新安装、发现、升级/卸载；从用户 PATH 调用安装产物。 |
| DST-04 | Toolkit Skill 从唯一来源独立通过 gh skill 安装，与 CLI 安装分离；来源 ref、版本和兼容性可追溯。 | 实际 gh skill 版本及参数核对；真实 harness 加载 Skill 并调用 PATH 中 CLI，保存 Skill 加载与 CLI 调用记录。 |
| DST-05 | Skill 只放工具事实、限制和有限用例；实验方法、统计与任务规划由 Agent 选择。 | 审查主 Skill 与渐进引用；验证 Agent 根据任务选择工具和基线。 |
| DST-06 | CLI/Mod/Skill/agent-hooks 的版本与协议兼容矩阵有来源提交、构建 hash、真实环境和未测项。实现、合并、发行与消费者验收分别记录。 | 使用发布资产的干净消费者与源码构建分别验；验收结果绑定实际 commit/hash 与发行组合。 |
| DST-07 | 全重写清除旧 Python Bridge、MCP、legacy loop 生产入口、依赖和活跃引用；保留历史与必要外部开发工具，逐项迁移功能。 | dependency/entrypoint/调用方扫描；基本链路仅 Go + Mod；所有旧能力有承接或有依据的范围决定。 |
| DST-08 | 旧命令、联合 Skill 安装、配置/缓存/快照格式的兼容、弃用与迁移有说明；升级保留用户世界、Skill 和凭证。 | 从指定旧版升级；旧参数明确引导/拒绝，新入口可用；兼容配置可迁移，格式冲突明确拒绝并引导用户。 |

## 安装与接口边界

Skill 独立安装，来源维护在 cli 仓库。首版建议放 cli/skills，Skill 名和发布 ref 后续确定。发行说明使用所验证 gh skill 版本的实际安装入口。

开发/验收可以使用 Python、脚本和独立 Minecraft 实例；产品运行组件为 Go 二进制与 Mod。平台支持通过实际安装验收确认。
