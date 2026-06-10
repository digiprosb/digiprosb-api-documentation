# E-wallet Direct Purchase

Transaksi e-wallet lewat `POST /purchase` — contoh **request**, **respons utama**, **callback sukses**, dan referensi **kode respons (RC)**.

## URL & autentikasi

**Endpoint**

```
https://indotechapi.socx.app/reseller/api/v1/purchase
```

**Header**

```http
Authorization: Bearer <JWT>
Content-Type: application/json
```

## Request

**Body (JSON)**

```json
{
  "code": "CDANA5",
  "msisdn": "085776810414",
  "request_id": "260313232300"
}
```

## Respons

#### Pending (contoh, `rc = 68`)

```json
{
  "code": "CDANA5",
  "msisdn": "085776810414",
  "request_id": "260313232300",
  "trxid": 3745717,
  "price": 10185,
  "rc": "68",
  "balance": 3653,
  "message": "PENDING, Transaksi sedang diproses"
}
```

Transaksi **belum final** saat `rc = 68`. Tunggu **callback** untuk hasil akhirnya.

### Callback sukses (contoh, `rc = 00`)

```json
{
  "data": {
    "ref_id": "260313232300",
    "status": "1",
    "code": "CDANA5",
    "hp": "085776810414",
    "price": "4545",
    "message": "Success",
    "balance": "7658690",
    "tr_id": "909649",
    "rc": "00",
    "sn": "TopUp DANA-FEBXXX VIAXX HERXXXXX/4500/085776810414/Reff:2025112510121481030100166579732735641"
  }
}
```

| Field | Keterangan |
|-------|------------|
| `ref_id` | Referensi Request   |
| `hp` | Echo nomor tujuan (`msisdn` pada request) |
| `tr_id` | ID transaksi di platform |
| `rc` | `00` = sukses |

### RC & respons lain

Daftar lengkap kode hasil (`rc`), pending (`68`), dan error: **[Kode respons (RC)](kode-respons.md)**.

---

## Catatan

- Alur **DANA dengan inquiry** (`POST /inquiry` → `POST /payment`) terpisah: [DANA — Inquiry → Payment](../ewallet/dana-inquiry.md).
- Hindari dobel-update status: gunakan `request_id` / `trxid` sebagai kunci idempotensi di sistem Anda.
