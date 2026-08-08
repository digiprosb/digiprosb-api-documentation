# DANA (Inquiry) — Fixed denom

An example of **fixed denom** (`code`: `DANA`, `idpel`: `{msisdn}#{nominal}`) is on the main full-flow page:

**[Ewallet Open Amount](e-wallet-open-amount.md)**

Inquiry-only summary (without the payment step):

```bash
curl -L -X POST 'https://api.digiprosb.id/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600000"}'
```

See also: [Open denom](dana-inquiry-denom-bebas.md)
