# Response codes (RC)

The `rc` field in the JSON response describes the transaction result.

## Response payload (JSON)

For **`POST /purchase`** and **`POST /status`**, the response body uses **JSON** with the following common fields. Concrete values (e.g. `message`, `sn`) depend on the product and scenario; see also [PREPAID — Pulsa & Data](./pembelian-pulsa-data.md), [Game & Voucher Top-up](../game/topup-voucher.md), and [ewallet purchase](../ewallet/ewallet-direct-purchase.md).

| Field | Type | Description |
|-------|------|-------------|
| `code` | string | Product code that was processed |
| `msisdn` | string | Destination number / ID (echo from the request if applicable) |
| `request_id` | string | Echo of your `request_id` |
| `rc` | string | Result code — see the table below |
| `trxid` | number | Transaction ID on the platform side; may be `0` on early failure (verify before go-live) |
| `price` | number | Price charged for this transaction |
| `balance` | number | Your deposit balance after the operation (per API policy) |
| `sn` | string | Serial / biller reference / voucher; may be empty when pending or failed |
| `message` | string | Human-readable description (status, error) |

### Example — success (`rc = 00`)

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

### Example — pending (`rc = 68`)

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

### Example — failed (RC 23)

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "99832748999",
  "rc": "23",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "",
  "message": "GAGAL, transaksi gagal di biller"
}
```

## Notes

- Connections are held for a maximum of 120 seconds. Configure your HTTP client with a timeout of at least 130 seconds.
- If the transaction fails immediately before pending (insufficient balance, product closed, etc.), the response is returned right away.
- On timeout (RC `68`), use the [Check status](cek-status.md) API to check the final status.
- Maximum 50 active sync connections per reseller. If exceeded, the server returns RC `68` with an informative message.

## RC code list

| RC | Description | Status |
|----|-------------|--------|
| `00` | SUCCESS | Success |
| `01` | Invalid payload | Failed |
| `02` | Invalid authorization | Failed |
| `03` | Transaction timeout | Failed |
| `05` | Product code not recognized | Failed |
| `06` | Biller connection issue | Failed |
| `07` | Customer number not found | Failed |
| `08` | Internal error | Failed |
| `09` | System under maintenance | Failed |
| `10` | Invalid ref code | Failed |
| `11` | Transaction not found | Failed |
| `12` | Customer number expired | Failed |
| `13` | Customer number blocked | Failed |
| `14` | Biller issue | Failed |
| `17` | Duplicate reversal transaction | Failed |
| `18` | Insufficient deposit balance | Failed |
| `19` | Product price not set | Failed |
| `21` | Refund | Failed |
| `22` | Product temporarily closed | Failed |
| `23` | Biller failure | Failed |
| `24` | Provider currently disrupted, please try again shortly | Failed |
| `25` | Product not registered in reseller group | Failed |
| `35` | System cut off in progress | Failed |
| `36` | Account reached maximum provider limit | Failed |
| `68` | Transaction pending, awaiting callback | **Pending** |
| `70` | Biller failure | Failed |
| `71` | Account suspended | Failed |
| `72` | Daily transaction limit reached | Failed |
| `73` | Product is not PPOB | Failed |
| `74` | Product not configured | Failed |
| `75` | Product currently disrupted | Failed |
| `76` | Transaction not found | Failed |
| `77` | Destination number not allowed | Failed |
| `78` | This product can only be purchased using unit balance (mode=unit) | Failed |
| `79` | [API v2] payment_ref expired — please inquiry again | Failed |
| `80` | [API v2] Bill amount changed since inquiry — payment_ref invalidated, inquiry again (balance not deducted) | Failed |
| `81` | [API v2] payment_ref already used by another payment (single-use) | Failed |
| `100` | Bill already paid | Failed |
| `101` | No bill | Failed |
| `102` | Invalid number | Failed |
| `114` | [PLN] The IDPEL you entered is incorrect, please check carefully. | Failed |
| `115` | [PLN] The meter number you entered is incorrect, please check carefully. | Failed |
| `177` | [PLN] Customer number blocked | Failed |
| `241` | [PLN] Minimum purchase Rp. 20 thousand | Failed |
| `247` | [PLN] Total KWH exceeds maximum limit | Failed |
| `268` | [PLN] Transaction failed | Failed |
| `290` | [PLN] Cutoff process in progress, please try again shortly | Failed |
| `293` | [PLN] Transaction failed | Failed |
