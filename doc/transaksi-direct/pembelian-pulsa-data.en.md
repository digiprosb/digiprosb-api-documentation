# Prepaid — Pulsa & Data

Prepaid transactions (pulsa and data) via `POST /purchase` — sample **request**, **response**, and **callback**. Full RC list: [Response codes (RC)](kode-respons.md).

## URL & authentication

**Base URL**

```
https://api.digiprosb.id/reseller/api/v1
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

### Response

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

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

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

### Response

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

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

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

| Field | Description |
|-------|-------------|
| `ref_id` | Echo of `request_id` from the request |
| `hp` | Echo of the destination number (`msisdn` in the request) |
| `tr_id` | Transaction ID on the platform |
| `sn` | Serial / biller reference — store for the customer |
| `rc` | `00` = success |

---

## Notes

- Failed responses and other codes: [Response codes (RC)](kode-respons.md).
- Avoid double status updates: use `request_id` / `trxid` as the idempotency key in your system.
