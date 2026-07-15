# DANA (Inquiry) — Denom Bebas

Contoh inquiry DANA denom bebas (open amount):

```json
{
  "code": "CDANA",
  "idpel": "082218965846#5000",
  "request_id": "26032972396000"
}
```

Contoh respons:

```json
{
  "code": "DANA_BEBAS",
  "idpel": "082218965846#5000",
  "request_id": "26032972396000",
  "product_name": "DANA Denom Bebas",
  "client_name": "DNID SANXX SUSXXXXXXX",
  "info": null,
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "1",
  "denda": "",
  "tagihan": "5000",
  "admin": "0",
  "total": "5000",
  "balance": 4412869
}
```

Setelah inquiry sukses, lanjut **`POST /payment`** dengan `code` / `idpel` yang sama dan `request_id` baru — lihat [Ewallet Open Amount](e-wallet-open-amount.md).

Lihat juga: [Denom tetap](dana-inquiry-denom-tetap.md)
