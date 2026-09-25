# Ewallet Open Amount V2

**E-wallet open amount V2** flow (inquiry → payment): validate and retrieve bill details via **`POST /inquiry`**, then pay via **`POST /payment`**.

> Previous version: [Ewallet Open Amount V1](e-wallet-open-amount.md)


## URL & authentication

**Base URL**

```
https://digiprosb.gw.socx.app/reseller/api/v1
```
**Header**      

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

## Payload data format

| Field | Required | Description |
|-------|----------|-------------|
| `code` | Yes | Product code, e.g. `DANA` |
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
 "code":"SDANA_BEBAS",
 "idpel":"089678549508#1000",
 "request_id":"250270202302301"
}

```

### Response

```json
{
    "code": "DANA_BEBAS",
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
 "code":"SDANA_BEBAS",
 "idpel":"089678549508#1000",
 "request_id":"2578072323871"
}
```

### Response

```json
{
    "code": "",
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

For open-amount products, `code` and `idpel` format follow the catalog (e.g. `CDANA`, `DANA_BEBAS`). The flow remains **inquiry → payment**; see the inquiry example in [Open denomination](dana-inquiry-denom-bebas.md).

## Difference from direct purchase

| Topic | E-wallet open amount | E-wallet direct purchase |
|-------|----------------------|---------------------------|
| Debit endpoint | `POST /payment` | `POST /purchase` |
| Pre-check | Required `POST /inquiry` | No |
| Destination field | `idpel` (`msisdn#nominal`) | `msisdn` + `code` |

Direct purchase without inquiry: [Ewallet Direct Purchase](ewallet-direct-purchase.md).
