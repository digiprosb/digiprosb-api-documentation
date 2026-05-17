# Dokumentasi API SOCX (Reseller H2H)

Dokumen ini untuk integrasi **Host-to-Host (H2H)** reseller ke platform SOCX. Isi disusun bertahap: **pengenalan & persiapan integrasi → transaksi → kode respons → contoh**.

## Isi dokumentasi

| Bagian | Keterangan |
|--------|------------|
| [Pengenalan & persiapan integrasi](02-persiapan-integrasi.md) | Gambaran API, base URL, autentikasi, whitelist, token, `request_id`, alur transaksi |
| **Transaksi direct purchase** | |
| → [PREPAID — Pulsa & Data](transaksi-direct/pembelian-pulsa-data.md) | `POST /purchase` prepaid: request & respons |
| → [Top Up & Voucher](game/topup-voucher.md) | `POST /purchase` game: request, klasifikasi, respons |
| → [Ewallet Direct Purchase](transaksi-direct/pembelian-ewallet.md) | `POST /purchase` e-wallet (request & respons) |
| → [PLN Prepaid](inquiry/inquiry-pln.md) | `POST /purchase` PLN Direct Purchase dan Direct with Inquiry  |
| → [Cek status](transaksi-direct/cek-status.md) | `POST /status` |
| → [Cek saldo](transaksi-direct/cek-saldo.md) | `GET /saldo` |
| → [Kode respons (RC)](transaksi-direct/kode-respons.md) | Tabel RC |
| [Lampiran — deposit tiket](appendix-deposit-ticket.md) | Di luar direct purchase; dari spesifikasi sumber |



