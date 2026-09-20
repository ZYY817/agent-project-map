# MAP.md — example index

> Minimal example of a root index. One line per area; details live in linked pages.

Small Express + React shop app. API in `server/`, UI in `web/`, SQLite via `server/db/`.

| Area | Purpose | Detail |
|---|---|---|
| Checkout | Cart → payment → order creation | [checkout](docs/map/checkout.md) |
| Orders | Order state machine, history views | [orders](docs/map/orders.md) |
| Auth | Session login, token refresh | [auth](docs/map/auth.md) |
| Shared UI | Design tokens, common components | `web/src/ui/` — no page yet |

Uncovered: `scripts/` admin tooling, email workers. Not mapped yet — treat as unknown.

---

## Example entry (from docs/map/checkout.md)

### Payment confirm

- **Aliases**: "付款成功但订单没动", checkout callback
- **Location**: `server/routes/payment.ts` → anchor: `handlePaymentCallback` (or error text `duplicate payment_id`)
- **Relations**: invoked by PSP webhook (`server/webhooks.ts` registers route); calls `orders/mark-paid.ts`; emits `order.paid` event consumed by `server/workers/notify.ts`
- **Constraints**: callback is retried by PSP — must be idempotent on `payment_id`; do not mark paid twice
- **Verify**: `pnpm test server/orders` + manual webhook replay script `scripts/replay-webhook.mjs`
- **Status**: verified — checked 2026-09-10 against commit `a1b2c3d`
