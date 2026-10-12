# 兼容性与交付设计

关联：DST-01…08。状态：安装形态已确认；名称、平台矩阵与版本规则待发行设计固定。

## 用户获得什么

必需项目运行物是一个 Go 二进制和一个 Fabric Mod JAR。Skill 独立安装；agent-hooks 接入按需配置。外部 harness 由用户选择和管理。

用户安装预编译二进制到 PATH。安装器说明当前 shell 与新 shell 的 PATH 行为、下载来源、版本 pin、校验、升级和卸载。Skill 通过独立安装入口部署到 harness。

## Skill 单一来源

建议唯一来源为 cli/skills 下的工具 Skill。使用 gh skill 安装，并记录 repo/ref/Skill 版本及实际消费的 harness。安装命令随 Skill 名、发布 ref 和所验证 gh 版本确定。

Skill 聚焦工具特有知识：参数、JSON、退出码、时钟、unknown、范围、资源限制和适用用例。工具用例与通用实验方法分别维护。通用方法指导可独立维护、按需加载。

## 版本维度

产品组合要列 CLI commit/version/hash、Mod commit/version/JAR hash、协议与快照格式、Skill ref/version、harness/profile 版本、游戏/Loader/API/Java 与 OS。发布组合随发行验收更新。

构建来源通过 commit/hash 识别，已发行 tag 与资产保留原内容，修复采用新版本。源码测试、真实游戏 E2E、下载校验和干净消费者验收分别维护。

## 全重写的兼容处理

新产品使用 MC Harness Bridge 入口，旧仓库保留需求与实现历史。Python/MCP/loop 的生产职责退出，仍有价值的功能在 [承接表](../traceability.md) 指定新归属。

旧联合安装参数、配置、缓存、manifest 和快照格式需明确兼容或拒绝及迁移方式。升级保留用户 Skill、世界和密钥，格式冲突明确拒绝并提供迁移路径。

## 首版支持范围

文档和目标 capability 对应实际支持环境与限制。未完成事项标记 planned/not-supported；平台支持关联安装验收记录。
