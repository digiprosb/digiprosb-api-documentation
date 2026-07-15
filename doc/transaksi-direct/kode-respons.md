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

### Contoh — gagal (`rc ≠ 00` dan bukan pending)

```json
{
  "code": "CTSEL5",
  "msisdn": "08100000000",
  "request_id": "PULSA-20250322-0002",
  "rc": "07",
  "trxid": 0,
  "price": 0,
  "balance": 341890000,
  "sn": "",
  "message": "Nomor pelanggan tidak ditemukan"
}
```

## Daftar kode RC

| RC | Keterangan | Status |
|----|------------|--------|
| `00` | Transaksi sukses | Berhasil |
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
| `35` | System cut off in progress | Gagal |
| `36` | Akun mencapai batas maksimal limit provider | Gagal |
| `68` | Transaksi pending, menunggu callback | **Pending** |
| `70` | Gagal biller | Gagal |
| `75` | Gagal | Gagal |

## Catatan implementasi

- **`68`**: anggap transaksi **belum final**; lanjutkan dengan [cek status](./cek-status.md) dan/atau callback (kontrak callback perlu dikonfirmasi oleh tim API).
- **`00`**: simpan `sn` jika ada sebagai bukti ke pelanggan.
- **`18`**: cek [cek saldo](./cek-saldo.md) sebelum retry.

