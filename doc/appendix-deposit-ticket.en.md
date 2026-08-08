# Appendix — Create deposit ticket

Outside the focus of **direct purchase**, but included in the source specification for integrator completeness.

## Request

| Property | Value |
|----------|--------|
| Method | `POST` |
| URL | `{base_url}/deposit_ticket` |
| Header | `Authorization: Bearer <JWT>` |
| Header | `Content-Type: application/json` |

## Body

| Field | Type | Required |
|-------|------|--------|
| `amount` | number | Yes |

## cURL example

```bash
curl -g --request POST \
  'https://api.digiprosb.id/reseller/api/v1/deposit_ticket' \
  --header 'Authorization: Bearer REPLACE-WITH-YOUR-JWT-TOKEN' \
  --header 'Content-Type: application/json' \
  --data-raw '{"amount":1000000}'
```

## Response (example)

```json
{
  "instruction": "Mohon transfer nominal Rp. 1,000,101 (harus sama), ke rekening BCA 1234567890, Mandiri 0987654321 sebelum 17/05/2024 01:37:08 Terima kasih",
  "amount": 1000000,
  "banks": [
    {
      "id": 1,
      "account_no": "1234567890",
      "bank_name": "BCA",
      "beneficiary_name": "Name",
      "status": 1
    },
    {
      "id": 2,
      "account_no": "0987654321",
      "bank_name": "Mandiri",
      "beneficiary_name": "Name",
      "status": 1
    }
  ],
  "unique": 101,
  "admin_fee": 0,
  "grand_total": 100101,
  "valid_before": "17/05/2024 01:37:08"
}
```

Validate the `banks` field in production, the date format, and whether the response is exactly the same — review with the Digiprosb team.
