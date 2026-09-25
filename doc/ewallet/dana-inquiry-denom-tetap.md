# DANA (Inquiry) — Denom tetap

Contoh **denom tetap** (`code`: `DANA`, `idpel`: `{msisdn}#{nominal}`) ada di halaman utama alur lengkap:

**[Ewallet Open Amount V1](e-wallet-open-amount.md)** · **[Ewallet Open Amount V2](e-wallet-open-amount-v2.md)**

Ringkasan inquiry saja (tanpa langkah payment):

```bash
curl -L -X POST 'https://api.digiprosb.id/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600000"}'
```

Lihat juga: [Denom bebas](dana-inquiry-denom-bebas.md)
