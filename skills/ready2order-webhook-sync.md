---
name: Subscribe to ready2order webhook events
description: Register a webhook URL and manage which POS events are pushed to your integration.
api: openapi/ready2order-openapi-original.json
operations: [webhookFind, webhookUpdateWebhookUrl, webhookFindWebhookEvents, webhookUpdateWebhookEvent]
---

# Subscribe to ready2order webhook events

## Auth
Send `Authorization: Bearer <ACCOUNT_TOKEN>`. Base URL: `https://api.ready2order.com/v1`.

## Steps
1. Inspect the current webhook config with `webhookFind` (`GET /webhook`).
2. Set/replace the receiving URL with `webhookUpdateWebhookUrl` (`PUT /webhook`).
3. List active and available events with `webhookFindWebhookEvents` (`GET /webhook/events`).
4. Add or remove an event with `webhookUpdateWebhookEvent` (`PUT /webhook/events`), passing `addEvent` or `removeEvent`.

## Events
`product.created/updated/deleted`, `productGroup.created/updated/deleted`, `customer.created/updated/deleted`, `coupon.created/updated`, `couponTransaction.created`, `invoice.created/cancelled`, `orderItem.created/cancelled/transferred`.

## Rules
- Events push the full object payload — no follow-up GET needed for basic sync.
- Endpoint must return 2xx quickly; do heavy work asynchronously.
