# Cek status

Mengambil status terkini transaksi berdasarkan `request_id` Anda.


## URL & autentikasi

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

| Properti | Nilai |
|----------|--------|
| Metode | `POST` |
| URL | `{base_url}/status` |
| Header | `Authorization: Bearer <JWT>` |
| Header | `Content-Type: application/json` |

## Body

| Field | Tipe | Wajib |
|-------|------|--------|
| `request_id` | string | Ya |

## Contoh Body

```json
{
  "request_id": "999999",
}
```

## Response (contoh)


### Sukses

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

### Gagal

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

## Praktik integrasi

1. Setelah purchase mengembalikan `rc = 68`, lakukan **polling** `/status` dengan interval yang wajar (mis. 2–5 detik, backoff maksimal) hingga `rc` final (`00` sukses atau kode gagal lain).

