# Game & Voucher Top-up

Game purchase (`POST /purchase`) — three categories, each with sample **request**, **response**, and **callback**. RC: [Response codes (RC)](../transaksi-direct/kode-respons.md).

## Purchase (`POST /purchase`)

**Endpoint**

```
https://api.digiprosb.id/reseller/api/v1/purchase
```

**Header**

```http
Authorization: Bearer <JWT>
Content-Type: application/json
```

**Body** — JSON: `code`, `msisdn`, `request_id`. The meaning of `msisdn` depends on the category below.

---

### Response fields (summary)

| Field | Description |
|-------|-------------|
| `code` | Product code |
| `rc` | Transaction result (`00` success, `68` pending, etc.) |
| `price` / `balance` | Price / balance |
| `sn` | Top-up: biller reference. Voucher: redeem code. |
| `message` | Status message |
| `trxid` / `tr_id` | Transaction ID |

Full RC list: [Response codes (RC)](../transaksi-direct/kode-respons.md).

---

## Game product classification

Three product categories:
- **Top-up without zone**
- **Top-up with zone**
- **Voucher**

## 1. Top-up without zone

Game list:
- Free Fire
- PUBG Mobile
- CODM
- Garena Undawn
- Honor of Kings
- Arena of Valor

| code | name | `msisdn` | `sn` (snippet) |
|------|------|----------|----------------|
| `CFF5` | Free Fire 5 Diamond CORP | `704899131` | nickname + refid … |

### Request

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760"
}
```

### Response

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760",
  "trxid": 2434954,
  "price": 900,
  "rc": "68",
  "balance": 47269920,
  "message": "PENDING, Transaksi sedang diproses"
}
```

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

### Callback

```json
{
  "data": {
    "ref_id": "eg45e10xpxge57760",
    "status": "1",
    "code": "CFF5",
    "hp": "704899131",
    "price": "900",
    "message": "Success",
    "balance": "47269920",
    "tr_id": "2434954",
    "rc": "00",
    "sn": "Free Fire 5 Diamonds /nickname : 死•ＩＲＦＡＮ•☠︎ refid: ab954b112f6c8aefbc6550167da150eb"
  }
}
```

---

## 2. Top-up with zone

- `msisdn` format: **user ID + zone** (combined, no spaces).
- Game list:
  - Mobile Legends: MLBB (`CML5`)

| code | name | `msisdn` | `sn` (snippet) |
|------|------|----------|----------------|
| `CML5` | MLBB 5 Diamonds … Corporate | `4189395759887` | `ZIYECH…` |

### Request

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066"
}
```

### Response

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066",
  "trxid": 2505577,
  "price": 1440,
  "rc": "68",
  "balance": 83844592,
  "message": "PENDING, Transaksi sedang diproses"
}
```

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

### Callback

```json
{
  "data": {
    "ref_id": "b624qp05nhnh52066",
    "status": "1",
    "code": "CML5",
    "hp": "4189395759887",
    "price": "1440",
    "message": "Success",
    "balance": "83844592",
    "tr_id": "2505577",
    "rc": "00",
    "sn": "ZIYECH. . RefId: CS774320333ZGVLM0U8VI"
  }
}
```

---

## 3. Voucher

`msisdn` = **phone number**. Successful `sn` = **redeem code**. Not a game ID.

- Google Play
- Roblox

| code | name | `msisdn` | `sn` (example) |
|------|------|----------|----------------|
| `GPC5` | Google Play Rp 5.000 … Corporate | `081386467468` | `03GCXLDRDPPNBBEL` |

### Request

```json
{
  "code": "GPC5",
  "msisdn": "081386467468",
  "request_id": "km17l40myg3z51097"
}
```

### Response

```json
{
  "code": "GPC5",
  "msisdn": "081386467468",
  "request_id": "km17l40myg3z51097",
  "trxid": 2209728,
  "price": 4900,
  "rc": "68",
  "balance": 59412105,
  "message": "PENDING, Transaksi sedang diproses"
}
```

The transaction is **not final** when `rc = 68`. Wait for the **callback** for the final result.

### Callback

```json
{
  "data": {
    "ref_id": "km17l40myg3z51097",
    "status": "1",
    "code": "GPC5",
    "hp": "081386467468",
    "price": "4900",
    "message": "Success",
    "balance": "59412105",
    "tr_id": "2209728",
    "rc": "00",
    "sn": "03GCXLDRDPPNBBEL"
  }
}
```

| Field | Description |
|-------|-------------|
| `ref_id` | Echo of `request_id` from the request |
| `hp` | Echo of destination number / ID (`msisdn` in the request) |
| `tr_id` | Transaction ID on the platform |
| `sn` | Top-up: biller reference. Voucher: redeem code. |
| `rc` | `00` = success |

---

## Notes

- Failed responses and other codes: [Response codes (RC)](../transaksi-direct/kode-respons.md).
- Avoid double status updates: use `request_id` / `trxid` as the idempotency key in your system.
