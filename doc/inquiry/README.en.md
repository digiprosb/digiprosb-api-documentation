# Inquiry & catalog

This section documents the **inquiry** endpoint (check customer data / product information before a transaction) and will be expanded for other product catalogs when available.

## Contents

| Page | Description |
|------|-------------|
| [PLN Prepaid](../pln-prepaid.md) | `POST /inquiry` — **PLN Prepaid** (`CPLN`) example, request & response |
| [Ewallet Open Amount V1](../ewallet/e-wallet-open-amount.md) | `POST /inquiry` then `POST /payment` (V1) |
| [Ewallet Open Amount V2](../ewallet/e-wallet-open-amount-v2.md) | `POST /inquiry` then `POST /payment` (V2) |

## Authentication & network

Same as other reseller APIs:

- Header **`Authorization: Bearer <JWT>`**
- **IP whitelist** for H2H production (see [Integration prep](../02-persiapan-integrasi.md))

**Base URL:** `https://api.digiprosb.id/reseller/api/v1` — inquiry: `POST .../inquiry`

## Recommended flow

1. **Inquiry** → validate customer / get display info (`info[]`) or bill details.
2. **Debit** → `POST /payment` (DANA) or `POST /purchase` (other categories) per product.

## Coming soon

- Full list of inquiry `code` values per category — from the Digiprosb team.
- Response variants for non-PLN products.

## Links to transactions

After inquiry, continue to the page for your category:
[Ewallet Open Amount V1](../ewallet/e-wallet-open-amount.md),
[Ewallet Open Amount V2](../ewallet/e-wallet-open-amount-v2.md),
[pulsa/data](../transaksi-direct/pembelian-pulsa-data.md),
[game — Topup Game & Voucher](../game/topup-voucher.md), or
[ewallet direct](../ewallet/ewallet-direct-purchase.md).
