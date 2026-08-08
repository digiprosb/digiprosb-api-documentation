# Check status

Retrieve the current transaction status by your `request_id`.


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

## Request

| Property | Value |
|----------|--------|
| Method | `POST` |
| URL | `{base_url}/status` |
| Header | `Authorization: Bearer <JWT>` |
| Header | `Content-Type: application/json` |

## Body

| Field | Type | Required |
|-------|------|----------|
| `request_id` | string | Yes |

## Body example

```json
{
  "request_id": "999999",
}
```

## Response (examples)


### Success

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "999999",
  "rc": "00",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "12345678901234567890",
  "message": "SUKSES"
}
```

### Failed

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "999999",
  "rc": "23",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "",
  "message": "Gagal, Gagal biller"
}
```

## Integration practices

1. After purchase returns `rc = 68`, **poll** `/status` at a reasonable interval (e.g. 2–5 seconds, with maximum backoff) until `rc` is final (`00` success or another failure code).
