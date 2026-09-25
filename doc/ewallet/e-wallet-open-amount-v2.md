# Ewallet Open Amount V2

Alur **e-wallet open amount V2** (inquiry → payment): validasi dan rincian tagihan lewat **`POST /inquiry`**, lalu pembayaran lewat **`POST /payment`**.

> Versi lama: [Ewallet Open Amount V1](e-wallet-open-amount.md)

Pada V2, **kode inquiry dan kode payment berbeda**:
- Inquiry: `DRYN_INQ`
- Payment: `DRYN02`


## URL & autentikasi

**Base URL**

```
https://digipro.gw.socx.app/reseller/api/v1
```
**Header**      

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

## Format Data Payload

| Field | Wajib | Keterangan |
|-------|-------|------------|
| `code` | Ya | Kode produk — inquiry: `DRYN_INQ`, payment: `DRYN02` |
| `idpel` | Ya | `{msisdn}#{nominal}` |
| `request_id` | Ya | ID unik dari sisi Anda |


Nomor tujuan dan nominal digabung dengan `#`:

```
{msisdn}#{nominal}
```

Contoh:

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

### Respons

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

### Respons

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

## Denom bebas

Untuk produk open amount V2, gunakan `code` inquiry `DRYN_INQ` dan `code` payment `DRYN02`. Format `idpel` tetap `{msisdn}#{nominal}`. Alur tetap **inquiry → payment**.

## 3. Cek status

Mengambil status terkini transaksi berdasarkan `request_id`.

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

### Respons sukses

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

### Respons gagal

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
