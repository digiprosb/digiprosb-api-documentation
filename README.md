# Dokumentasi API Indotech (Reseller H2H)

Repositori ini berisi **dokumentasi teknis** untuk integrasi **Host-to-Host (H2H)** antara sistem Anda dan platform **Indotech** sebagai reseller. Dokumen ditulis dalam Bahasa Indonesia dan diorganisir per **kategori produk** serta **referensi teknis** (selaras sidebar MkDocs).


### Pengenalan & persiapan integrasi

- [Satu halaman: pengenalan, checklist production, alur transaksi](doc/02-persiapan-integrasi.md)

- [Ringkasan PREPAID](doc/prepaid/README.md) — request & respon

### GAME

- [Ringkasan GAME](doc/game/README.md)
- [Top Up & Voucher](doc/game/topup-voucher.md) — pembelian, klasifikasi, contoh respons

### EWALLET

- [Ringkasan EWALLET](doc/ewallet/README.md)
- [DANA — inquiry → payment](doc/ewallet/dana-inquiry.md)

### Inquiry khusus

- [Inquiry PLN (`CPLN`)](doc/inquiry/inquiry-pln.md)

### Referensi teknis

- [Pengenalan & persiapan integrasi](doc/02-persiapan-integrasi.md)
- [Cek saldo](doc/transaksi-direct/cek-saldo.md) · [Pembelian Pulsa & Data](doc/transaksi-direct/pembelian-pulsa-data.md) · [Top Up & Voucher — game](doc/game/topup-voucher.md) · [Ewallet Direct Purchase](doc/transaksi-direct/pembelian-ewallet.md) · [Cek status](doc/transaksi-direct/cek-status.md)
- [Lampiran deposit tiket](doc/appendix-deposit-ticket.md)
- [Kode respons (RC)](doc/transaksi-direct/kode-respons.md)

**Beranda situs (MkDocs):** [doc/index.md](doc/index.md)

---

## Apa yang tercakup

| Area | Status | Keterangan |
|------|--------|------------|
| Pengenalan & persiapan integrasi | Tersedia | Base URL, auth, whitelist, `request_id`, diagram alur |
| PREPAID (pulsa, data) | Tersedia | Request & respon |
| GAME (top-up & voucher) | Tersedia | [Top Up & Voucher](doc/game/topup-voucher.md) — satu halaman |
| EWALLET (direct purchase, DANA inquiry → payment) | Tersedia | `POST /inquiry` + `POST /payment`; denom tetap & bebas |
| Inquiry PLN | Tersedia | Contoh `CPLN` |
| Direct purchase (JSON / HTTP) | Tersedia | `code`, `msisdn`, `request_id` |
| Cek saldo · status · RC | Tersedia | `GET /saldo`, `POST /status`, tabel RC |
| Deposit tiket | Lampiran | Di luar fokus direct purchase |
| Daftar harga / katalog lengkap | Menyusul | Perlu `code` resmi dari tim Indotech |

---

Detail lengkap: [Pengenalan & persiapan integrasi](doc/02-persiapan-integrasi.md).

---

## Daftar endpoint (quick reference)

| Metode | Path | Fungsi | Dokumentasi |
|--------|------|--------|-------------|
| `GET` | `/saldo` | Cek saldo deposit | [doc/transaksi-direct/cek-saldo.md](doc/transaksi-direct/cek-saldo.md) |
| `POST` | `/purchase` | Transaksi pembelian kategori prepaid | [doc/transaksi-direct/pembelian-pulsa-data.md](doc/transaksi-direct/pembelian-pulsa-data.md) |
| `POST` | `/purchase` | Transaksi pembelian kategori game | [doc/game/topup-voucher.md](doc/game/topup-voucher.md) |
| `POST` | `/purchase` | Ewallet Direct Purchase | [doc/transaksi-direct/pembelian-ewallet.md](doc/transaksi-direct/pembelian-ewallet.md) |
| `POST` | `/status` | Cek status by `request_id` | [doc/transaksi-direct/cek-status.md](doc/transaksi-direct/cek-status.md) |
| `POST` | `/deposit_ticket` | Buat tiket deposit | [doc/appendix-deposit-ticket.md](doc/appendix-deposit-ticket.md) |

**Idempotensi:** jika Anda mengirim ulang **`request_id` yang sama** dan transaksi itu sudah pernah diproses, API mengembalikan **respons yang sama** dengan transaksi tersebut (bukan transaksi baru).

**Pending (`rc = 68`):** transaksi diterima tetapi belum final; lanjutkan dengan polling **`/status`** dan/atau mekanisme callback jika sudah disepakati dengan tim Indotech (detail callback/XML `topUpReport` — review internal).

---

## Alur integrasi (disarankan)

1. **Persiapan:** whitelist IP, simpan JWT dengan aman, tentukan konvensi `request_id` (unik per order baru).
2. **Opsional:** `GET /saldo` sebelum transaksi besar.
3. **Purchase:** `POST /purchase` (atau jalur HTTP jika sistem Anda mengharuskan).
4. **Jika `rc = 68`:** panggil `POST /status` dengan interval wajar hingga status final (`00` atau kode gagal).
5. **Simpan** `trxid`, `request_id`, `sn` (jika ada) untuk rekonsiliasi dan dukungan pelanggan.

Alur: [Pengenalan & persiapan integrasi — bagian alur](doc/02-persiapan-integrasi.md#alur-transaksi) · [PREPAID — Pulsa & Data](doc/transaksi-direct/pembelian-pulsa-data.md) · [game](doc/game/README.md).

## Struktur repositori

```
.
├── README.md                 ← Pengantar repositori (Anda di sini)
├── mkdocs.yml                ← Navigasi situs (Material)
├── requirements-docs.txt
├── .gitignore
└── doc/
    ├── index.md              ← Beranda MkDocs
    ├── introduction-transaction-flow.md  ← pengalihan ke 02 (tautan lama)
    ├── 02-persiapan-integrasi.md         ← pengenalan + persiapan + alur
    ├── appendix-deposit-ticket.md
    ├── prepaid/              ← Pulsa, data
    ├── game/                 ← Top-up non-zone, zona, voucher
    ├── ewallet/              ← Direct purchase + DANA inquiry
    ├── inquiry/
    │   ├── README.md
    │   └── inquiry-pln.md    ← Contoh CPLN
    └── transaksi-direct/     ← Purchase, saldo, status, RC, klasifikasi game
```

---

## Lisensi & kontak

Hak cipta dan kebijakan distribusi dokumen mengikuti kebijakan **Indotech / pemilik API**. Untuk whitelist IP, kredensial API, atau pertanyaan integrasi, hubungi **tim teknis Indotech** melalui kanal resmi yang diberikan kepada mitra.

---

