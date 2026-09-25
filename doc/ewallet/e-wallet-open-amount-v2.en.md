# Ewallet Open Amount V2

**E-wallet open amount V2** flow (inquiry → payment): validate and retrieve bill details via **`POST /inquiry`**, then pay via **`POST /payment`**.

> Previous version: [Ewallet Open Amount V1](e-wallet-open-amount.md)

In V2, the **inquiry code and payment code are different**:
- Inquiry: `DRYN_INQ`
- Payment: `DRYN02`


## URL & authentication

**Base URL**

```
https://digipro.gw.socx.app/reseller/api/v1
```
**Header**      

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

## Payload data format

| Field | Required | Description |
|-------|----------|-------------|
| `code` | Yes | Product code — inquiry: `DRYN_INQ`, payment: `DRYN02` |
| `idpel` | Yes | `{msisdn}#{nominal}` |
| `request_id` | Yes | Unique ID from your side |


Destination number and amount are joined with `#`:

```
{msisdn}#{nominal}
```

Example:

## 1. Inquiry


### Request

**Endpoint:** `POST {base_url}/inquiry`


```bash
{
 "code":"DRYN_INQ",
 "idpel":"089678549508#1000",
 "request_id":"250270202302301"
}

```

### Response

```json
{
    "code": "DRYN_INQ",
    "idpel": "089678549508#1000",
    "request_id": "25027170202302301",
    "product_name": "DANA Denom Bebas",
    "client_name": "DNID MAUXXXX EGXXXX",
    "info": null,
    "rc": "00",
    "msg": "SUKSES",
    "jumlah_tagihan": "1",
    "denda": "",
    "tagihan": "1000",
    "admin": "700",
    "total": "1700",
    "balance": 2296814
}
```


## 2. Payment

**Endpoint:** `POST {base_url}/payment`

### Request


```bash
{
 "code":"DRYN02",
 "idpel":"089678549508#1000",
 "request_id":"2578072323871"
}
```

### Response

```json
{
    "code": "DRYN02",
    "idpel": "089678549508#1000",
    "request_id": "257807232323871",
    "product_name": "SALDO DANA BEBAS",
    "client_name": "DNID MAUXXXX EGXXXX",
    "info": null,
    "rc": "00",
    "msg": "SUKSES",
    "jumlah_tagihan": "1",
    "denda": "",
    "tagihan": "1000",
    "admin": "700",
    "total": "1700",
    "nomor_referensi": "DNID MAUXXXX EGXXXX/6289678549508/2026061010121481030100166091131018932",
    "trx_id": 3745398,
    "balance": 9793,
    "footer": "",
    "header": "Digiprosb",
    "time": "10/06/2026 08:08:46"
}
```

## Open denomination

For open-amount V2 products, use inquiry `code` `DRYN_INQ` and payment `code` `DRYN02`. The `idpel` format remains `{msisdn}#{nominal}`. The flow remains **inquiry → payment**.

## 3. Check status

Retrieve the current transaction status by `request_id`.

**Base URL**

```
https://digipro.gw.socx.app/reseller/api/v1
```

**Endpoint:** `POST {base_url}/status`

### Request

```json
{
  "request_id": "2578072323871"
}
```

### Success response

```json
{
  "code": "DRYN02",
  "msisdn": "089678549508#1000",
  "request_id": "2578072323871",
  "rc": "00",
  "trxid": 3745398,
  "price": 1700,
  "balance": 9793,
  "sn": "DNID MAUXXXX EGXXXX/6289678549508/2026061010121481030100166091131018932",
  "message": "SUKSES"
}
```

### Failed response

```json
{
  "code": "DRYN02",
  "msisdn": "089678549508#1000",
  "request_id": "2578072323871",
  "rc": "23",
  "trxid": 3745398,
  "price": 1700,
  "balance": 9793,
  "sn": "",
  "message": "Gagal, Gagal biller"
}
```
