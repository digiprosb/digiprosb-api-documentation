# Dokumentasi API SOCX (Reseller H2H)

Dokumen ini untuk integrasi **Host-to-Host (H2H)** reseller ke platform SOCX. Isi disusun bertahap: **pengenalan & persiapan integrasi → transaksi → kode respons → contoh**.

## Isi dokumentasi

| Bagian | Keterangan |
|--------|------------|
| [Pengenalan & persiapan integrasi](02-persiapan-integrasi.md) | Gambaran API, base URL, autentikasi, whitelist, token, `request_id`, alur transaksi |
| **Transaksi direct purchase** | |
| → [PREPAID — Pulsa & Data](transaksi-direct/pembelian-pulsa-data.md) | `POST /purchase` prepaid: request, respons & callback |
| → [Topup Game & Voucher](game/topup-voucher.md) | `POST /purchase` game: request, respons & callback |
| → [Ewallet Direct Purchase](ewallet/ewallet-direct-purchase.md) | `POST /purchase` e-wallet: request, respons & callback |
| → [Ewallet Open Amount](ewallet/e-wallet-open-amount.md) | `POST /inquiry` lalu `POST /payment`: request & respons |
| → [PLN Prepaid](pln-prepaid.md) | `POST /purchase` PLN Direct Purchase dan Direct with Inquiry  |
| → [Cek status](transaksi-direct/cek-status.md) | `POST /status` |
| → [Cek saldo](transaksi-direct/cek-saldo.md) | `GET /saldo` |
| → [Kode respons (RC)](transaksi-direct/kode-respons.md) | Tabel RC |
| [Lampiran — deposit tiket](appendix-deposit-ticket.md) | Di luar direct purchase; dari spesifikasi sumber |



