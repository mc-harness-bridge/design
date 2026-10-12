# 上下文与实体数据契约

关联：CTX-01…06。状态：覆盖约束；格式待正式协议确定。

## 现场引用

聊天事件绑定捕获时的 sender、source、context_id 和 capture phase。Agent 取回得到同一 bundle；live query 是另一次采样。bundle 保存紧凑现场，实体与世界数据按需查询。

receipt、broadcast fallback 和捕获失败分别表达来源与时点。context_id 绑定玩家和 run，取回对应 bundle。

缓存至少公布容量策略、TTL、最大 bundle 和过期/逐出语义。引用失效返回 expired/not_found 或等效结构化状态；live query 使用独立入口。

## 玩家视线

输入明确玩家、距离和适用规则；服务端从眼位和朝向查询 block/entity/miss。遮挡、无碰撞可选方块、实体在方块后和 unknown player 必须覆盖。数据标明服务端视线来源和采样时点。

## NBT/order 捕获

- 明确维度、源运行、取样时点、实体集合范围和遗漏条件。
- 受支持实体保留 UUID、type、NBT、tick order、passengers、vehicle 与 root 元数据。
- 普通实体状态保留完整的受支持原生 NBT。
- 玩家排除、不同步实体、未加载区域和截断分别声明。
- 文件行序/明确 order、游戏 tick 顺序和空间查询顺序分别定义。
- orderHash 校验声明集合的顺序；跨实体行为另以游戏观测验收。

实体导出要能被普通终端工具读取。骑乘关系可能在 NBT 和外层元数据重复，必须固定哪一处权威、如何避免重复加载；验证循环/缺失引用和 root 范围。

旧实现曾拒绝 radius 并按维度捕获。新设计保留明确集合与范围的能力目标，若增加筛选须另行定义其对 tick order、骑乘树和截断的影响，导出标明实际筛选范围。
