# Top Up & Voucher

Purchase game (`POST /purchase`) — tiga kategori, masing-masing dengan contoh **request** dan **respons**. RC: [Kode respons (RC)](../transaksi-direct/kode-respons.md).

## Pembelian (`POST /purchase`)

**Endpoint**

```
https://indotechapi.socx.app/reseller/api/v1/purchase
```

**Header**

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

**Body** — JSON: `code`, `msisdn`, `request_id`. Arti `msisdn` tergantung kategori di bawah.

---

### Field respons (ringkas)

| Field | Keterangan |
|-------|------------|
| `code` | Kode produk |
| `rc` | Hasil transaksi (`00` sukses, `68` pending, dll.) |
| `price` / `balance` | Harga / saldo |
| `sn` | Top-up: referensi biller. Voucher: kode redeem. |
| `message` | Pesan status |
| `trxid` / `tr_id` | ID transaksi |

RC lengkap: [Kode respons (RC)](../transaksi-direct/kode-respons.md).

---

## Klasifikasi produk game

Tiga kategori produk:
- **Top-up tanpa zona**
- **Top-up dengan zona**
- **Voucher**

## 1. Top-up Non zona

Daftar game:
- Free Fire
- PUBG Mobile
- CODM
- Garena Undawn
- Honor of Kings
- Arena of Valor

| code | nama | `msisdn` | `sn` (cuplikan) |
|------|------|----------|-----------------|
| `CFF5` | Free Fire 5 Diamond CORP | `704899131` | nickname + refid … |

### Request

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760"
}
```

### Respons sukses (contoh)

```json
{
  "ref_id": "eg45e10xpxge57760",
  "status": "1",
  "code": "CFF5",
  "hp": "704899131",
  "price": "900",
  "message": "Success",
  "balance": "47269920",
  "tr_id": "2434954",
  "rc": "00",
  "sn": "Free Fire 5 Diamonds /nickname : 死•ＩＲＦＡＮ•☠︎ refid: ab954b112f6c8aefbc6550167da150eb"
}
```

HTTP mengikuti [Pembelian](#pembelian-post-purchase) (Base URL, header, `POST /purchase`).

---

## 2. Top-up With zona

- Format `msisdn`: **user ID + zone** (dijadikan satu, tanpa spasi).
- Daftar game:
  - Mobile Legends: MLBB (`CML5`)


| code | nama | `msisdn` | `sn` (cuplikan) |
|------|------|----------|-----------------|
| `CML5` | MLBB 5 Diamonds … Corporate | `4189395759887` | `ZIYECH…` |

### Request

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066"
}
```

### Respons pending (contoh, `rc=68`)

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066",
  "rc": "68",
  "trxid": 2505577,
  "price": 1440,
  "balance": 83844592,
  "message": "PENDING, Transaksi sedang diproses"
}
```

### Respons sukses (contoh)

```json
{
  "ref_id": "b624qp05nhnh52066",
  "status": "1",
  "code": "CML5",
  "hp": "4189395759887",
  "price": "1440",
  "message": "Success",
  "balance": "83844592",
  "tr_id": "2505577",
  "rc": "00",
  "sn": "ZIYECH. . RefId: CS774320333ZGVLM0U8VI"
}
```

HTTP mengikuti [Pembelian](#pembelian-post-purchase).

---

## 3. Voucher

`msisdn` = **nomor HP**. `sn` sukses = **kode redeem**. Bukan ID game.

- Google Play
- Roblox

| code | nama | `msisdn` | `sn` (contoh) |
|------|------|----------|---------------|
| `GPC5` | Google Play Rp 5.000 … Corporate | `081386467468` | `03GCXLDRDPPNBBEL` |

### Request

```json
{
  "code": "GPC5",
  "msisdn": "081386467468",
  "request_id": "km17l40myg3z51097"
}
```

### Respons sukses (contoh)

```json
{
  "ref_id": "km17l40myg3z51097",
  "status": "1",
  "code": "GPC5",
  "hp": "081386467468",
  "price": "4900",
  "message": "Success",
  "balance": "59412105",
  "tr_id": "2209728",
  "rc": "00",
  "sn": "03GCXLDRDPPNBBEL"
}
```

HTTP mengikuti [Pembelian](#pembelian-post-purchase).


