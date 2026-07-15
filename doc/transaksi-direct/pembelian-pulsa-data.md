# Prepaid — Pulsa & Data

Transaksi prepaid (pulsa dan data) lewat `POST /purchase` — contoh **request**, **respons**, dan **callback**. RC lengkap: [Kode respons (RC)](kode-respons.md).

## URL & autentikasi

**Base URL**

```
https://indotechapi.socx.app/reseller/api/v1
```

**Header**

```http
Authorization: Bearer <JWT>
Content-Type: application/json
```

---

## Pulsa

### Request

```json
{
  "code": "CTSEL5",
  "msisdn": "081234567890",
  "request_id": "26031600002200"
}
```

### Respons

```json
{
  "code": "CTSEL5",
  "msisdn": "081234567890",
  "request_id": "26031600002200",
  "trxid": 2421510,
  "price": 5450,
  "rc": "68",
  "balance": 120995,
  "message": "PENDING, Transaksi sedang diproses"
}
```

Transaksi **belum final** saat `rc = 68`. Tunggu **callback** untuk hasil akhirnya.

### Callback

```json
{
  "data": {
    "ref_id": "26031600002200",
    "status": "1",
    "code": "CTSEL5",
    "hp": "081234567890",
    "price": "5450",
    "message": "Success",
    "balance": "120995",
    "tr_id": "2421510",
    "rc": "00",
    "sn": "04092900001248875319"
  }
}
```

---

## Data

### Request

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201"
}
```

### Respons

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201",
  "trxid": 2421511,
  "price": 14950,
  "rc": "68",
  "balance": 115545,
  "message": "PENDING, Transaksi sedang diproses"
}
```

Transaksi **belum final** saat `rc = 68`. Tunggu **callback** untuk hasil akhirnya.

### Callback

```json
{
  "data": {
    "ref_id": "26031600002201",
    "status": "1",
    "code": "CTMINI13",
    "hp": "082121250591",
    "price": "14950",
    "message": "Success",
    "balance": "115545",
    "tr_id": "2421511",
    "rc": "00",
    "sn": "04042000001595621715"
  }
}
```

| Field | Keterangan |
|-------|------------|
| `ref_id` | Echo `request_id` dari request |
| `hp` | Echo nomor tujuan (`msisdn` pada request) |
| `tr_id` | ID transaksi di platform |
| `sn` | Serial / referensi biller — simpan untuk pelanggan |
| `rc` | `00` = sukses |

---

## Catatan

- Respons gagal dan kode lain: [Kode respons (RC)](kode-respons.md).
- Hindari dobel-update status: gunakan `request_id` / `trxid` sebagai kunci idempotensi di sistem Anda.
