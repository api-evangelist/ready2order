---
name: Manage the ready2order product catalog
description: Create product groups and products, and keep stock levels in sync, in a ready2order POS account.
api: openapi/ready2order-openapi-original.json
operations: [productGroupCreate, productCreate, productCreateBatch, productGetStock, productUpdateStock, productUpdateStockInBatch]
---

# Manage the ready2order product catalog

Use the ready2order Public API v1 to build and maintain the point-of-sale catalog.

## Auth
Every request sends `Authorization: Bearer <ACCOUNT_TOKEN>`. Obtain the Account Token via the three-token flow (Developer Token -> Grant Access Token -> Account Token). Base URL: `https://api.ready2order.com/v1`.

## Steps
1. Create a product group with `productGroupCreate` (`POST /productgroups`) to organize the menu/catalog.
2. Create products with `productCreate` (`POST /products`), setting the product group id. For large imports use `productCreateBatch` (`POST /products/batch`).
3. Read current stock with `productGetStock` (`GET /products/{id}/stock`).
4. Adjust stock with `productUpdateStock` (`PUT /products/{id}/stock`), or bulk with `productUpdateStockInBatch` (`POST /products/batch/stock`).

## Rules
- Paginate list calls with `page` / `limit` / `offset`.
- Respect the rate limit of 60 requests/minute per Account Token; on `429` back off and retry.
- Subscribe to `product.created` / `product.updated` webhook events to stay in sync instead of polling.
