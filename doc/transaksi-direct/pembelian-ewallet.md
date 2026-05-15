# E-wallet Direct Purchase

Transaksi e-wallet lewat `POST /purchase` — contoh **request**, **respons sukses**, dan referensi **kode respons (RC)**.

**Endpoint**

```
https://indotechapi.socx.app/reseller/api/v1/purchase
```

**Header**

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

---

## Request

**Body (JSON)**

```json
{
  "code": "CDANA5",
  "msisdn": "085776810414",
  "request_id": "26032500001001"
}
```


## Respons

### Sukses (contoh, `rc=00`)

```json
{
  "data": {
    "ref_id": "qi46fh0jwcsp58268",
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

### RC & respons lain

Daftar lengkap kode hasil (`rc`), pending (`68`), dan error: **[Kode respons (RC)](kode-respons.md)**.

---

## Catatan

- Alur **DANA dengan inquiry** (`POST /inquiry` → `POST /payment`) terpisah: [DANA — Inquiry → Payment](../ewallet/dana-inquiry.md).
