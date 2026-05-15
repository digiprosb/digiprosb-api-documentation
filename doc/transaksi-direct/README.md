# Transaksi — Direct purchase

Bagian ini fokus pada alur **pembelian langsung** (top-up / voucher). Ringkasan alur tingkat dokumen ada di **[Pengenalan & persiapan integrasi](../02-persiapan-integrasi.md#alur-transaksi)**.

## Alur disarankan

1. **Cek saldo** (opsional tapi dianjurkan sebelum transaksi besar): [`GET /saldo`](./cek-saldo.md)
2. **Purchase** — pilih satu jalur:
   - [`POST /purchase` pulsa/data](./pembelian-pulsa-data.md)
   - [`POST /purchase` game — Top Up & Voucher](../game/topup-voucher.md)
   - [Ewallet Direct Purchase](./pembelian-ewallet.md)
3. Jika `rc = 68` (**pending**): polling [`POST /status`](./cek-status.md) sampai final, atau tunggu **callback** (kontrak callback perlu dikonfirmasi — lihat contoh pending di [PREPAID — Pulsa & Data](./pembelian-pulsa-data.md)).

## Isi folder

| File | Isi |
|------|-----|
| [cek-saldo.md](./cek-saldo.md) | GET saldo |
| [pembelian-pulsa-data.md](./pembelian-pulsa-data.md) | PREPAID — Pulsa & Data: request & respons |
| [../game/topup-voucher.md](../game/topup-voucher.md) | Game: purchase, klasifikasi, contoh respons |
| [pembelian-ewallet.md](./pembelian-ewallet.md) | Ewallet Direct Purchase — request, respons, RC |
| [cek-status.md](./cek-status.md) | POST status |
| [kode-respons.md](./kode-respons.md) | Tabel RC |
| [flow-direct-purchase-without-inquiry.md](./flow-direct-purchase-without-inquiry.md) | Alur & diagram direct purchase **tanpa** inquiry |
| [payment-with-inquiry.md](./payment-with-inquiry.md) | payment with inquiry — alur, diagram, referensi produk |

Deposit tiket (`/deposit_ticket`) ada di spesifikasi sumber tetapi di luar fokus **direct purchase**; dapat ditambahkan halaman terpisah jika dibutuhkan.


