# Check balance

Real-time check of the reseller deposit balance.

## URL & authentication

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

| Property | Value |
|----------|--------|
| Method | `GET` |
| URL | `{base_url}/saldo` |
| Header | `Authorization: Bearer <JWT>` |


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
