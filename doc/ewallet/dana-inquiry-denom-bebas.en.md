# DANA (Inquiry) — Open Denom

Example DANA open denom (open amount) inquiry:

```json
{
  "code": "CDANA",
  "idpel": "082218965846#5000",
  "request_id": "26032972396000"
}
```

Example response:

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

After a successful inquiry, continue with **`POST /payment`** using the same `code` / `idpel` and a new `request_id` — see [Ewallet Open Amount](e-wallet-open-amount.md).

See also: [Fixed denom](dana-inquiry-denom-tetap.md)
