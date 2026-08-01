---
name: Create customers and issue bills
description: Register a customer and create, retrieve, and print a bill/invoice in ready2order.
api: openapi/ready2order-openapi-original.json
operations: [customerCreate, customerFindById, billCreateBill, billFindById, billPrint, billPdf]
---

# Create customers and issue bills

## Auth
Send `Authorization: Bearer <ACCOUNT_TOKEN>` on every request. Base URL: `https://api.ready2order.com/v1`.

## Steps
1. Create a customer with `customerCreate` (`POST /customers`); retrieve later with `customerFindById` (`GET /customers/{id}`).
2. Create a bill with `billCreateBill` (`POST /document/invoice`), referencing the customer where applicable.
3. Retrieve it with `billFindById` (`GET /document/invoice/{id}`).
4. Print it with `billPrint` (`POST /document/invoice/{id}/print`) or fetch the PDF with `billPdf` (`GET /document/invoice/{id}/pdf`).

## Rules
- Bills are legally relevant (AT/DE/CH fiscal compliance); cancel via `billDelete` (`POST /document/invoice/{id}/delete`) rather than deleting records.
- No idempotency-key is supported — guard against duplicate POSTs client-side.
- Listen for `invoice.created` / `invoice.cancelled` / `customer.created` webhook events.
