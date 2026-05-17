
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

## PLN Direct Purchase

## Purchase

**Endpoint:** `POST {base_url}/purchase`

### Request

```json
 {
  "code": "PLP20",
  "msisdn": "86070364095",
  "request_id": "3399862"
}
```

### Respons

```json
{
  "data": {
    "ref_id": "dfypn0ec0knkts44",
    "status": "1",
    "code": "PLP20",
    "hp": "86070364095",
    "price": "21745",
    "message": "Success",
    "balance": "96145806",
    "tr_id": "3399862",
    "rc": "00",
    "sn_raw": "STRUK PEMBELIAN LISTRIK PRABAYAR@NO_METER:86070364095@IDPEL:431900257347@NAMA:KADIR BE'Y@ADMIN_BANK:0@TARIF_DAYA:R1/450 VA@NO_REF:40D708E987FE41E1A13A4AD592437932@RP_BAYAR:20000@MATERAI:0@PPN:0@PPJ:1819@ANGSURAN:0@RP_STROOM_TOKEN:18181@JML_KWH:43,9@STROOM_TOKEN:5065-4980-9887-7667-8924@INFO:INFORMASI HUBUNGI CALL CENTER 123 ATAU HUBUNGI PLN TERDEKAT[][AM]20000[]",
    "parsed": {
      "no_meter": "86070364095",
      "id_pelanggan": "431900257347",
      "nama": "KADIR BE'Y",
      "tarif_daya": "R1/450 VA",
      "no_ref": "40D708E987FE41E1A13A4AD592437932",
      "rp_bayar": 20000,
      "materai": 0,
      "ppn": 0,
      "ppj": 1819,
      "angsuran": 0,
      "rp_stroom_token": 18181,
      "kwh": "43,9",
      "stroom_token": "5065-4980-9887-7667-8924"
    }
  }
}
```


## PLN Direct with Inquiry

## Inquiry 

**Endpoint:** `POST {base_url}/inquiry`

### Request

```bash
  {
    "code":"CPLN",
    "idpel":"121021034831",
    "request_id":"250717000000"
  }
```

### Response

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


## Purchase

**Endpoint:** `POST {base_url}/purchase`

### Request


```bash
{
  "code": "PLP20",
  "msisdn": "45130152445",
  "request_id": "3400013"
}
```

### Respons

```json
{
  "code": "PLP20",
  "msisdn": "45130152445",
  "request_id": "3400013",
  "trxid": 40232480,
  "price": 21725,
  "rc": "00",
  "balance": 3429004,
  "message": "SUKSES",
  "data": {
    "sn_raw": "STRUK PEMBELIAN LISTRIK PRABAYAR@NO_METER:45130152445@IDPEL:432560019605@NAMA:WAGEL ADOLF LANI@ADMIN_BANK:0@TARIF_DAYA:R1/450 VA@NO_REF:97C1EBC8A2F34E3EBB758D6655D784FA@RP_BAYAR:20000@MATERAI:0@PPN:0@PPJ:1819@ANGSURAN:0@RP_STROOM_TOKEN:18181@JML_KWH:43,9@STROOM_TOKEN:5461-6433-4860-7756-8839@INFO:INFORMASI HUBUNGI CALL CENTER 123 ATAU HUBUNGI PLN TERDEKAT[][AM]20000[]",
    "parsed": {
      "no_meter": "45130152445",
      "id_pelanggan": "432560019605",
      "nama": "WAGEL ADOLF LANI",
      "tarif_daya": "R1/450 VA",
      "no_ref": "97C1EBC8A2F34E3EBB758D6655D784FA",
      "rp_bayar": 20000,
      "materai": 0,
      "ppn": 0,
      "ppj": 1819,
      "angsuran": 0,
      "rp_stroom_token": 18181,
      "kwh": "43,9",
      "stroom_token": "5461-6433-4860-7756-8839"
    }
  }
}
```

