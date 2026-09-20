# MAP.md — 索引示例

> 根索引的最小示例。每个模块一行；细节在链接的子页里。

Express + React 小商城。API 在 `server/`，界面在 `web/`，SQLite 在 `server/db/`。

| 模块 | 用途 | 详情 |
|---|---|---|
| 下单结算 | 购物车 → 支付 → 生成订单 | [checkout](docs/map/checkout.md) |
| 订单 | 订单状态机、历史查看 | [orders](docs/map/orders.md) |
| 登录 | 会话登录、令牌刷新 | [auth](docs/map/auth.md) |
| 共用组件 | 设计变量、通用组件 | `web/src/ui/`——暂无子页 |

未覆盖：`scripts/` 管理工具、邮件 worker。还没画——按未知对待。

---

## 条目示例（摘自 docs/map/checkout.md）

### 支付回调确认

- **别名**："付款成功但订单没动"、checkout callback
- **位置**：`server/routes/payment.ts` → 锚点：`handlePaymentCallback`（或报错原文 `duplicate payment_id`）
- **关系**：由 PSP 的 webhook 触发（`server/webhooks.ts` 注册路由）；调用 `orders/mark-paid.ts`；发出 `order.paid` 事件，被 `server/workers/notify.ts` 消费
- **约束**：回调会被 PSP 重试——必须按 `payment_id` 幂等，不许重复标记已支付
- **验证**：`pnpm test server/orders` + 手动重放脚本 `scripts/replay-webhook.mjs`
- **状态**：已核对——2026-09-10 对照提交 `a1b2c3d`
