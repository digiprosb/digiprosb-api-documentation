# Inquiry & katalog

Bagian ini mendokumentasikan endpoint **inquiry** (cek data pelanggan / informasi produk sebelum transaksi) dan akan diperluas untuk katalog produk lain jika tersedia.

## Isi

| Halaman | Keterangan |
|---------|------------|
| [Inquiry PLN](inquiry-pln.md) | `POST /inquiry` — contoh **PLN Prabayar** (`CPLN`), request & response |
| [Ewallet Open Amount](../ewallet/e-wallet-open-amount.md) | `POST /inquiry` lalu `POST /payment` |

## Autentikasi & jaringan

Sama seperti API reseller lainnya:

- Header **`Authorization: Bearer <JWT>`**
- **Whitelist IP** untuk H2H production (lihat [Persiapan integrasi](../02-persiapan-integrasi.md))

**Base URL:** `https://indotechapi.socx.app/reseller/api/v1` — inquiry: `POST .../inquiry`

## Alur disarankan

1. **Inquiry** → validasi pelanggan / ambil info tampilan (`info[]`) atau rincian tagihan.
2. **Debit** → `POST /payment` (DANA) atau `POST /purchase` (kategori lain) sesuai produk.

## Menyusul

- Daftar lengkap `code` inquiry per kategori — dari tim SOCX.
- Varian response untuk produk non-PLN.

## Link ke transaksi

Setelah inquiry, lanjut ke halaman sesuai kategori:
[Ewallet Open Amount](../ewallet/e-wallet-open-amount.md),
[pulsa/data](../transaksi-direct/pembelian-pulsa-data.md),
[game — Top Up & Voucher](../game/topup-voucher.md), atau
[ewallet direct](../transaksi-direct/pembelian-ewallet.md).
