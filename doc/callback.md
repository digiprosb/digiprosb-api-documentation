# Callback

## Ringkasan

Callback adalah sebuah metode di mana sebuah sistem akan secara otomatis mengirimkan informasi atau notifikasi kepada URL yang telah ditentukan setelah suatu proses atau transaksi selesai diproses.


## HTTP Request

| Properti | Nilai |
|----------|--------|
| Metode | `POST` |
| Content-Type | `application/json` |

## URL Callback

```http
POST {callback_url}
```

## Payload Callback

### Contoh respons sukses

```json
{
  "code": "DRYN02",
  "msisdn": "089674950955#100",
  "request_id": "25071w2123q12700001",
  "trxid": 13170,
  "price": 180,
  "rc": "00",
  "balance": 0,
  "sn": "DNID MAUXXXX EGXXXXX",
  "message": "SUKSES"
}
```

### Contoh respons gagal

```json
{
  "code": "DRYN02",
  "msisdn": "0896774950955#100",
  "request_id": "0015fk5qwixoa5fj",
  "trxid": 17,
  "price": 800,
  "rc": "23",
  "balance": 45700,
  "message": "Gagal, Gagal biller"
}
```

## Deskripsi parameter

| Parameter | Keterangan |
|-----------|------------|
| `code` | Kode produk |
| `msisdn` | Nomor tujuan pelanggan |
| `request_id` | Identitas permintaan transaksi dari sisi client |
| `trxid` | Identitas transaksi yang diberikan oleh server kami |
| `price` | Nominal / harga transaksi |
| `rc` | Kode respons transaksi |
| `balance` | Sisa saldo |
| `sn` | Nomor serial / referensi (tersedia pada transaksi sukses) |
| `message` | Pesan status transaksi |

Daftar lengkap nilai `rc`: [Kode respons (RC)](transaksi-direct/kode-respons.md).

## Respons callback / acknowledgement

Penerima callback boleh mengembalikan respons HTTP sebagai tanda bahwa request callback telah diterima.

**Contoh:**

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "status": "success"
}
```

Acknowledgement ini **tidak** digunakan untuk memicu pemrosesan lanjutan 

## Kebijakan retry

Callback tidak menerapkan mekanisme retry otomatis.

Jika pengiriman callback gagal karena timeout, gangguan jaringan, atau HTTP response yang tidak berhasil, callback tidak akan dikirim ulang secara otomatis oleh sistem.

Jika diperlukan, notifikasi callback dapat dikirim ulang secara manual dari sistem.

Jika status akhir transaksi belum diterima, gunakan API Cek Status (POST /status) dengan request_id yang sama untuk mendapatkan status transaksi terbaru.

