# DANA (Inquiry) — Denom tetap

Contoh **denom tetap** (`code`: `DANA`, `idpel`: `{msisdn}#{nominal}`) ada di halaman utama alur lengkap:

**[Ewallet Open Amount](e-wallet-open-amount.md)**

Ringkasan inquiry saja (tanpa langkah payment):

```bash
curl -L -X POST 'https://indotechapi.socx.app/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600000"}'
```

Lihat juga: [Denom bebas](dana-inquiry-denom-bebas.md)
