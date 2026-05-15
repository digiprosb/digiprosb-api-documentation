# Inquiry PLN

## Request

```bash
curl -L -X POST 'https://indotechapi.socx.app/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"CPLN","idpel":"121021034831","request_id":"250717000000"}'
```

## Response

```json
{
  "code": "CPLN",
  "idpel": "121021034831",
  "request_id": "250717000000",
  "product_name": "Inquiry PLN Prabayar",
  "client_name": "NRML~!@ $^*}?-&.PROD#TEST2",
  "info": [
    {
      "name": "Nomor",
      "value": "08102138831"
    },
    {
      "name": "Nama",
      "value": "NRML~!@ $^*}?-&.PROD#TEST2"
    },
    {
      "name": "Tarif/Daya",
      "value": "R1/900"
    },
    {
      "name": "Stroom/Token Unsold",
      "value": "0"
    }
  ],
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "",
  "denda": "",
  "tagihan": "",
  "admin": "",
  "total": "",
  "balance": 29986594769
}
```
