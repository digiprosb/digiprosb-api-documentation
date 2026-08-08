# Transactions — Direct purchase

This section focuses on the **direct purchase** flow (top-up / voucher). A document-level flow summary is in **[Introduction & integration prep](../02-persiapan-integrasi.md#transaction-flow)**.

## Recommended flow

1. **Check balance** (optional but recommended before large transactions): [`GET /saldo`](./cek-saldo.md)
2. **Purchase** — choose one path:
   - [`POST /purchase` pulsa/data](./pembelian-pulsa-data.md)
   - [`POST /purchase` game — Topup Game & Voucher](../game/topup-voucher.md)
   - [Ewallet Direct Purchase](../ewallet/ewallet-direct-purchase.md)
3. If `rc = 68` (**pending**): poll [`POST /status`](./cek-status.md) until final, or wait for **callback** (callback contract must be confirmed — see pending examples in [PREPAID — Pulsa & Data](./pembelian-pulsa-data.md)).

## Folder contents

| File | Contents |
|------|----------|
| [cek-saldo.md](./cek-saldo.md) | GET balance |
| [pembelian-pulsa-data.md](./pembelian-pulsa-data.md) | PREPAID — Pulsa & Data: request & response |
| [../game/topup-voucher.md](../game/topup-voucher.md) | Game: Topup Game & Voucher — purchase, classification, response examples |
| [Ewallet Direct Purchase](../ewallet/ewallet-direct-purchase.md) | Ewallet Direct Purchase — request, response, RC |
| [cek-status.md](./cek-status.md) | POST status |
| [kode-respons.md](./kode-respons.md) | RC table |
| [flow-direct-purchase-without-inquiry.md](./flow-direct-purchase-without-inquiry.md) | Flow & diagram for direct purchase **without** inquiry |
| [payment-with-inquiry.md](./payment-with-inquiry.md) | payment with inquiry — flow, diagram, product references |

Deposit ticket (`/deposit_ticket`) exists in the source specification but is outside the **direct purchase** focus; a separate page can be added if needed.
