# Prepaid — Pulsa & Data

Transaksi prepaid (pulsa dan data) — **request**, **respons**. RC lengkap: [Kode respons (RC)](kode-respons.md).

## URL & autentikasi

**Base URL**

```
https://indotechapi.socx.app/reseller/api/v1
```
**Header**

```
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
  "rc": "00",
  "balance": 120995,
  "sn": "04092900001248875319",
  "message": "SUKSES"
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


---


### Respon

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201",
  "trxid": 2421511,
  "price": 14950,
  "rc": "00",
  "balance": 115545,
  "sn": "04042000001595621715",
  "message": "SUKSES"
}
```

---

## Catatan

- Respons gagal dan kode lain: [Kode respons (RC)](kode-respons.md).
