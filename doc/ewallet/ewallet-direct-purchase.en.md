# Ewallet Direct Purchase

E-wallet transactions via `POST /purchase` — sample **request**, **response**, and **callback**. RC: [Response codes (RC)](../transaksi-direct/kode-respons.md).

## URL & authentication

**Endpoint**

```
https://api.digiprosb.id/reseller/api/v1/purchase
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

## Response

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

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

## Callback


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

| Field | Description |
|-------|-------------|
| `ref_id` | Request reference |
| `hp` | Echo of the destination number (`msisdn` in the request) |
| `tr_id` | Transaction ID on the platform |
| `rc` | `00` = success |

### Other RCs & responses

Full list of result codes (`rc`), pending (`68`), and errors: **[Response codes (RC)](../transaksi-direct/kode-respons.md)**.

---

## Notes

- The **e-wallet open amount** flow (`POST /inquiry` → `POST /payment`) is separate: [Ewallet Open Amount](e-wallet-open-amount.md).
- Avoid double status updates: use `request_id` / `trxid` as the idempotency key in your system.
