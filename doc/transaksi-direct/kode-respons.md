# Kode respons (RC)

Kode `rc` pada respons JSON menggambarkan hasil transaksi.

## Payload respons (JSON)

Untuk **`POST /purchase`** dan **`POST /status`**, body respons memakai **JSON** dengan field umum berikut. Nilai konkret (mis. `message`, `sn`) mengikuti produk dan skenario; lihat juga [PREPAID — Pulsa & Data](./pembelian-pulsa-data.md), [Topup Game & Voucher](../game/topup-voucher.md), dan [pembelian ewallet](./pembelian-ewallet.md).

| Field | Tipe | Keterangan |
|-------|------|------------|
| `code` | string | Kode produk yang diproses |
| `msisdn` | string | Nomor / ID tujuan (echo dari request jika relevan) |
| `request_id` | string | Echo `request_id` Anda |
| `rc` | string | Kode hasil — lihat tabel di bawah |
| `trxid` | number | ID transaksi di sisi platform; bisa `0` saat gagal awal (verifikasi sebelum go-live) |
| `price` | number | Harga yang dikenakan untuk transaksi ini |
| `balance` | number | Saldo deposit Anda setelah operasi (sesuai kebijakan API) |
| `sn` | string | Serial / referensi biller / voucher; bisa kosong saat pending atau gagal |
| `message` | string | Deskripsi human-readable (status, error) |

### Contoh — sukses (`rc = 00`)

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "PULSA-20250322-0001",
  "rc": "00",
  "trxid": 16413,
  "price": 5400,
  "balance": 341884600,
  "sn": "02123123123123123",
  "message": "SUKSES"
}
```

### Contoh — pending (`rc = 68`)

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "PULSA-20250322-0001",
  "rc": "68",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "",
  "message": "PENDING, Transaksi sedang diproses"
}
```

### Contoh — gagal  (RC 23)

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "99832748999",
  "rc": "23",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "",
  "message": "GAGAL, transaksi gagal di biller"
}
```

## Catatan

- Koneksi ditahan maksimal 120 detik. Konfigurasikan HTTP client Anda dengan timeout minimal 130 detik.
- Jika transaksi langsung gagal sebelum pending (saldo tidak cukup, produk tutup, dll), response dikembalikan segera.
- Jika terjadi timeout (RC `68`), gunakan API [Cek status](cek-status.md) untuk mengecek status akhir.
- Maksimal 50 koneksi sync aktif per reseller. Jika melebihi, server return RC `68` dengan pesan informatif.

## Daftar kode RC
 
| RC | Keterangan | Status |
|----|------------|--------|
| `00` | SUKSES | Berhasil |
| `01` | Invalid payload | Gagal |
| `02` | Invalid authorization | Gagal |
| `03` | Transaksi timeout | Gagal |
| `05` | Kode produk tidak dikenali | Gagal |
| `06` | Gangguan koneksi biller | Gagal |
| `07` | Nomor pelanggan tidak ditemukan | Gagal |
| `08` | Internal error | Gagal |
| `09` | Sistem dalam proses pemeliharaan | Gagal |
| `10` | Ref code tidak valid | Gagal |
| `11` | Transaksi tidak ditemukan | Gagal |
| `12` | Nomor pelanggan kadaluarsa | Gagal |
| `13` | Nomor pelanggan diblokir | Gagal |
| `14` | Gangguan biller | Gagal |
| `17` | Duplikasi transaksi reversal | Gagal |
| `18` | Saldo deposit tidak cukup | Gagal |
| `19` | Harga produk belum diset | Gagal |
| `21` | Refund | Gagal |
| `22` | Produk sementara ditutup | Gagal |
| `23` | Gagal biller | Gagal |
| `24` | Provider sedang gangguan, silakan coba beberapa saat lagi | Gagal |
| `25` | Produk tidak terdaftar di grup reseller | Gagal |
| `35` | System cut off in progress | Gagal |
| `36` | Akun mencapai batas maksimal limit provider | Gagal |
| `68` | Transaksi pending, menunggu callback | **Pending** |
| `70` | Gagal biller | Gagal |
| `71` | Akun disuspend | Gagal |
| `72` | Batas transaksi harian tercapai | Gagal |
| `73` | Produk bukan PPOB | Gagal |
| `74` | Produk belum disetting | Gagal |
| `75` | Produk sedang gangguan | Gagal |
| `76` | Transaksi tidak ditemukan | Gagal |
| `77` | Nomor tujuan tidak diizinkan | Gagal |
| `78` | Produk ini hanya bisa dibeli menggunakan saldo unit (mode=unit) | Gagal |
| `79` | [API v2] payment_ref kadaluarsa — silakan inquiry ulang | Gagal |
| `80` | [API v2] Nominal tagihan berubah sejak inquiry — payment_ref hangus, inquiry ulang (saldo tidak terpotong) | Gagal |
| `81` | [API v2] payment_ref sudah dipakai payment lain (single-use) | Gagal |
| `100` | Tagihan sudah terbayar | Gagal |
| `101` | Tidak ada tagihan | Gagal |
| `102` | Nomor tidak valid | Gagal |
| `114` | [PLN] IDPEL yang anda masukkan salah, mohon teliti kembali. | Gagal |
| `115` | [PLN] Nomor meter yang anda masukkan salah, mohon teliti kembali. | Gagal |
| `177` | [PLN] Nomor pelanggan diblokir | Gagal |
| `241` | [PLN] Pembelian minimal Rp. 20 ribu | Gagal |
| `247` | [PLN] Total KWH melebihi batas maksimum | Gagal |
| `268` | [PLN] Transaksi gagal | Gagal |
| `290` | [PLN] Sedang berlangsung proses cutoff, silahkan coba beberapa saat kemudian | Gagal |
| `293` | [PLN] Transaksi gagal | Gagal |



