# Ewallet Open Amount

Alur **e-wallet open amount** (inquiry → payment): validasi dan rincian tagihan lewat **`POST /inquiry`**, lalu pembayaran lewat **`POST /payment`**.


## URL & autentikasi

**Base URL**

```
https://xxx/reseller/api/v1
```
**Header**

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

## Format Data Payload

| Field | Wajib | Keterangan |
|-------|-------|------------|
| `code` | Ya | Kode produk, contoh: `DANA` |
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
 "code":"SDANA_BEBAS",
 "idpel":"089678549508#1000",
 "request_id":"250270202302301"
}

```

### Respons

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
    "admin": "485",
    "total": "1485",
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

### Respons

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
    "admin": "485",
    "total": "1485",
    "nomor_referensi": "DNID MAUXXXX EGXXXX/6289678549508/2026061010121481030100166091131018932",
    "trx_id": 3745398,
    "balance": 9793,
    "footer": "",
    "header": "Digiprosb",
    "time": "10/06/2026 08:08:46"
}
```

## Denom bebas

Untuk produk open amount, `code` dan format `idpel` mengikuti katalog (contoh `CDANA`, `DANA_BEBAS`). Alur tetap **inquiry → payment**; lihat contoh inquiry di [Denom bebas](dana-inquiry-denom-bebas.md).

## Perbedaan dengan direct purchase

| Topik | E-wallet open amount | E-wallet direct purchase |
|-------|----------------------|---------------------------|
| Endpoint debit | `POST /payment` | `POST /purchase` |
| Pra-cek | Wajib `POST /inquiry` | Tidak |
| Field tujuan | `idpel` (`msisdn#nominal`) | `msisdn` + `code` |

Direct purchase tanpa inquiry: [Ewallet Direct Purchase](../transaksi-direct/pembelian-ewallet.md).
