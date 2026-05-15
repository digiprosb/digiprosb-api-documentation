# Dokumentasi API SOCX (Reseller H2H)

Dokumen ini untuk integrasi **Host-to-Host (H2H)** reseller ke platform SOCX. Isi disusun bertahap: **pengenalan & persiapan integrasi → transaksi → kode respons → contoh**.

## Isi dokumentasi

| Bagian | Keterangan |
|--------|------------|
| [Pengenalan & persiapan integrasi](02-persiapan-integrasi.md) | Gambaran API, base URL, autentikasi, whitelist, token, `request_id`, alur transaksi |
| **Transaksi direct purchase** | |
| → [Cek saldo](transaksi-direct/cek-saldo.md) | `GET /saldo` |
| → [PREPAID — Pulsa & Data](transaksi-direct/pembelian-pulsa-data.md) | `POST /purchase` prepaid: request & respons |
| → [Top Up & Voucher — game (POST)](game/topup-voucher.md) | `POST /purchase` game: request, klasifikasi, respons |
| → [Ewallet Direct Purchase](transaksi-direct/pembelian-ewallet.md) | `POST /purchase` e-wallet (request & respons) |
| → [Cek status](transaksi-direct/cek-status.md) | `POST /status` |
| → [Kode respons (RC)](transaksi-direct/kode-respons.md) | Tabel RC |
| [Inquiry](inquiry/README.md) | `POST /inquiry` — contoh PLN prabayar (`CPLN`) |
| [Lampiran — deposit tiket](appendix-deposit-ticket.md) | Di luar direct purchase; dari spesifikasi sumber |

## Status dokumen

- **Siap dipakai untuk integrasi:** direct purchase (JSON/HTTP), cek saldo, cek status, tabel RC — sesuai sumber internal `socx.md`.
- **Perlu review tim SOCX / API:** callback setelah `rc = 68` (pending), verifikasi webhook/XML `topUpReport`, URL & kontrak **inquiry** / daftar harga, finalisasi parameter game per `code` di tabel klasifikasi.


