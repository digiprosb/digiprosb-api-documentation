# Check status

Retrieve the current transaction status by your `request_id`.

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

## cURL example

```bash
curl -g --request POST \
  'https://api.digiprosb.id/reseller/api/v1/status' \
  --header 'Authorization: Bearer REPLACE-WITH-YOUR-JWT-TOKEN' \
  --header 'Content-Type: application/json' \
  --data-raw '{"request_id":"999999"}'
```

## Response (examples)

Format is the **same** as the purchase response.

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

## Errors

- `rc = 11` — transaction not found (see [response codes](./kode-respons.md)).
