# Webhook 与 Hermes 接入设计

关联：HOK-01…06、EVT-01…04。状态：原生 Hermes V2 是承接目标；新产品尚未实现。

## 仓库归属

cli 拥有唯一生产 HTTP 投递器、队列、重试、接收方 profile 和签名实现。agent-hooks 维护所验证接收方协议、配置样例、测试 fixture、真实互操作 runbook 与版本记录。fixture receiver 仅用于测试/诊断，不成为常驻生产转签组件。

这种拆分让接入资料和验收可以独立更新，又不制造第二套 runtime。若新增接收方需要代码，生产部分仍通过 cli PR 交付，agent-hooks PR 补接入与证据。

## 接收方 profile

通用签名模式和 Hermes V2 分开命名、协商和版本化。固定真实 Hermes 版本/提交，核对准确的签名输入字节、header、timestamp 单位/窗口、delivery ID、JSON body/type、过滤和 route 匹配。

旧通用模式使用 HMAC-SHA256 对 timestamp 与 body bytes 签名，可以作为迁移来源；不能默认 Hermes 使用相同拼接和 header。具体字段以实际接收端和 fixture 为准。

事件 ID 与投递 ID 区分：一次事件面向一个目标的逻辑投递有稳定 ID；重试沿用 ID。时间与签名是否每次尝试更新，以接收方契约决定；不得更新 ID 来绕开去重。

## 交付状态

queued、attempting、HTTP accepted、retry exhausted、dropped 等是投递事实。Agent run started、tool called、reply delivered 属于真实接收方验收证据；HTTP 2xx 不证明任务完成。

没有持久队列时 daemon 重启可能丢待投递事件，必须在状态和文档中写明。接收成功后响应丢失，靠稳定 ID 和所验证接收方去重窗口避免重复触发；不扩大为无限时间恰好一次。

## 配置与操作边界

默认禁用。用户配置 endpoint、过滤、签名/凭证来源和上限；状态输出只显示必要非秘密信息。route、模型、工具权限、Gateway 启动和回复目标归用户/harness，产品不代管。

真实 Hermes 验收至少涵盖正确/错误/过期签名、匹配事件、响应丢失重试、Skill 消费、CLI 调用和回复目标。所有结果绑定确切版本与配置。
