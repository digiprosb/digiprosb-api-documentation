# DANA — Inquiry → Payment (post paid)

Alur **DANA with inquiry**: validasi dan rincian tagihan lewat **`POST /inquiry`**, lalu pembayaran lewat **`POST /payment`**.


## URL & autentikasi

**Base URL**

```
https://indotechapi.socx.app/reseller/api/v1
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
curl -L -X POST 'https://indotechapi.socx.app/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600000"}'
```

### Respons

```json
{
  "code": "DANA",
  "idpel": "08996647676#1000",
  "request_id": "26032600000",
  "product_name": "DANA",
  "client_name": "DNID aXX danX",
  "info": null,
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "1",
  "denda": "",
  "tagihan": "1000",
  "admin": "60",
  "total": "1060",
  "balance": 29986574717
}
```


## 2. Payment

**Endpoint:** `POST {base_url}/payment`

### Request

| Field | Wajib | Keterangan |
|-------|-------|------------|
| `code` | Ya | Sama dengan inquiry, contoh: `DANA` |
| `idpel` | Ya | Sama dengan inquiry |
| `request_id` | Ya | ID unik **baru** untuk payment |

```bash
curl -L -X POST 'https://indotechapi.socx.app/reseller/api/v1/payment' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600001"}'
```

### Respons

```json
{
  "code": "",
  "idpel": "08996647676#1000",
  "request_id": "26032600001",
  "product_name": "DANA",
  "client_name": "DNID aXX danX",
  "info": null,
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "",
  "denda": "",
  "tagihan": "",
  "admin": "",
  "total": "",
  "nomor_referensi": "DNID aXX danX/628996647676/2026032610121481030100166434401355494",
  "trx_id": 202277,
  "balance": 29986573667,
  "footer": "",
  "header": "SOCX",
  "time": "26/03/2026 19:27:54"
}
```

## Denom bebas

Untuk produk open amount, `code` dan format `idpel` mengikuti katalog (contoh `CDANA`, `DANA_BEBAS`). Alur tetap **inquiry → payment**; lihat contoh inquiry di [Denom bebas](dana-inquiry-denom-bebas.md).

## Perbedaan dengan direct purchase

| Topik | DANA inquiry → payment | E-wallet direct purchase |
|-------|------------------------|---------------------------|
| Endpoint debit | `POST /payment` | `POST /purchase` |
| Pra-cek | Wajib `POST /inquiry` | Tidak |
| Field tujuan | `idpel` (`msisdn#nominal`) | `msisdn` + `code` |

Direct purchase tanpa inquiry: [Ewallet Direct Purchase](../transaksi-direct/pembelian-ewallet.md).
