# Digiprosb API Documentation (Reseller H2H)

This document covers **Host-to-Host (H2H)** reseller integration with the Digiprosb platform. Content is organized in stages: **introduction & integration prep → transactions → response codes → examples**.

## Documentation contents

| Section | Description |
|--------|------------|
| [Introduction & integration prep](02-persiapan-integrasi.md) | API overview, base URL, authentication, whitelist, token, `request_id`, transaction flow |
| **Direct purchase transactions** | |
| → [PREPAID — Pulsa & Data](transaksi-direct/pembelian-pulsa-data.md) | `POST /purchase` prepaid: request, response & callback |
| → [Game & Voucher Topup](game/topup-voucher.md) | `POST /purchase` game: request, response & callback |
| → [Ewallet Direct Purchase](ewallet/ewallet-direct-purchase.md) | `POST /purchase` e-wallet: request, response & callback |
| → [Ewallet Open Amount V1](ewallet/e-wallet-open-amount.md) | `POST /inquiry` then `POST /payment` (legacy base URL) |
| → [Ewallet Open Amount V2](ewallet/e-wallet-open-amount-v2.md) | `POST /inquiry` then `POST /payment` (new base URL) |
| → [PLN Prepaid](pln-prepaid.md) | `POST /purchase` PLN Direct Purchase and Direct with Inquiry  |
| → [Check status](transaksi-direct/cek-status.md) | `POST /status` |
| → [Check balance](transaksi-direct/cek-saldo.md) | `GET /saldo` |
| → [Callback](callback.md) | Final transaction result notification for `POST /purchase` |
| → [Response codes (RC)](transaksi-direct/kode-respons.md) | RC table |
| [Appendix — deposit ticket](appendix-deposit-ticket.md) | Outside direct purchase; from the source specification |

