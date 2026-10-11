# 兼容性与交付设计

关联：DST-01…08。状态：安装形态已确认；名称、平台矩阵与版本规则待发行设计固定。

## 用户获得什么

必需项目运行物是一个 Go 二进制和一个 Fabric Mod JAR。Skill 独立安装；agent-hooks 接入按需配置。不会安装 Python Bridge、模型 SDK、MCP 服务或项目自己的 Agent loop。

二进制进入用户 PATH，不要求 Go 编译环境。安装器说明当前 shell 与新 shell 的 PATH 行为、下载来源、版本 pin、校验、升级和卸载。二进制安装不维护各 harness 私有 Skill 目录。

## Skill 单一来源

建议唯一来源为 cli/skills 下的工具 Skill。使用 gh skill 安装，并记录 repo/ref/Skill 版本及实际消费的 harness。实际 CLI 参数由已验证 gh 版本的帮助确定，不把未实现 Skill 名或 URL 写成当前安装命令。

Skill 聚焦工具特有知识：参数、JSON、退出码、时钟、unknown、范围、资源限制和适用用例。示例不能借引用链默认加载通用实验方法。外部可选方法指导是否创建，由独立证据决定，本轮不增加仓库。

## 版本维度

产品组合要列 CLI commit/version/hash、Mod commit/version/JAR hash、协议与快照格式、Skill ref/version、harness/profile 版本、游戏/Loader/API/Java 与 OS。代码合并不自动更新发布组合。

版本字符串不是来源：不同 commit/hash 的构建即使显示同一版本，也必须分别记录。tag 和 release 资产不能悄悄覆盖。源码测试、真实游戏 E2E、下载校验和干净消费者验收分别维护。

## 全重写的兼容处理

旧仓库命名已不作为新产品入口；不擅自删除/转移旧仓库或改写历史。Python/MCP/loop 的生产职责退出，仍有价值的功能在 [承接表](../traceability.md) 指定新归属。

旧联合安装参数、配置、缓存、manifest 和快照格式需明确兼容或拒绝及迁移方式。不能自动读取旧版本不兼容数据，也不能在升级时无说明删除用户 Skill、世界或密钥。

## 首版能力宣传

新增能力必须在真实目标 capability 中可用，文档写明支持环境和限制。未完成事项保留为 planned/not-supported。只构建出跨平台文件时，不宣传所有平台安装已验证。
