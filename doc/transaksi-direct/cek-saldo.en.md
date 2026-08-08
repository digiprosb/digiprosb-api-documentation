# Check balance

Real-time check of the reseller deposit balance.

## Request

| Property | Value |
|----------|--------|
| Method | `GET` |
| URL | `{base_url}/saldo` |
| Header | `Authorization: Bearer <JWT>` |

## cURL example

```bash
curl -g --request GET \
  'https://api.digiprosb.id/reseller/api/v1/saldo' \
  --header 'Authorization: Bearer REPLACE-WITH-YOUR-JWT-TOKEN'
```

## Success response (example)

```json
{
  "balance": 14450
}
```

| Field | Type | Description |
|-------|------|-------------|
| `balance` | number | Available balance (unit per Digiprosb internal contract — usually whole-number rupiah) |

## Common errors

See [response codes](./kode-respons.md) for RCs that appear on transaction endpoints. For `/saldo`, authentication failures follow the general API pattern (error body format if not 200 — confirm with the API team).
