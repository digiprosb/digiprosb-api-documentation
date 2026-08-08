# Cek saldo

Pengecekan saldo deposit reseller secara real-time.

## URL & autentikasi

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

| Properti | Nilai |
|----------|--------|
| Metode | `GET` |
| URL | `{base_url}/saldo` |
| Header | `Authorization: Bearer <JWT>` |


## Response sukses (contoh)

```json
{
  "balance": 14450
}
```

| Field | Tipe | Keterangan |
|-------|------|------------|
| `balance` | number | Saldo tersedia (satuan sesuai kontrak internal Digiprosb — biasanya rupiah whole number) |

## Error umum

Lihat [kode respons](./kode-respons.md) untuk RC yang muncul pada endpoint transaksi. Untuk `/saldo`, kegagalan autentikasi mengikuti pola API umum (format body error jika bukan 200 — perlu konfirmasi tim API).
