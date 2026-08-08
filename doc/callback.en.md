# Callback

## Overview

A callback is a method in which a system automatically sends information or a notification to a predetermined URL after a process or transaction has finished processing.


## HTTP Request

| Property | Value |
|----------|--------|
| Method | `POST` |
| Content-Type | `application/json` |

## Callback URL

```http
POST {callback_url}
```

## Callback payload

### Success response example

```json
{
  "code": "DRYN02",
  "msisdn": "089674950955#100",
  "request_id": "25071w2123q12700001",
  "trxid": 13170,
  "price": 180,
  "rc": "00",
  "balance": 0,
  "sn": "DNID MAUXXXX EGXXXXX",
  "message": "SUKSES"
}
```

### Failed response example

```json
{
  "code": "DRYN02",
  "msisdn": "0896774950955#100",
  "request_id": "0015fk5qwixoa5fj",
  "trxid": 17,
  "price": 800,
  "rc": "23",
  "balance": 45700,
  "message": "Gagal, Gagal biller"
}
```

## Parameter description

| Parameter | Description |
|-----------|------------|
| `code` | Product code |
| `msisdn` | Customer destination number |
| `request_id` | Transaction request identity from the client side |
| `trxid` | Transaction identity assigned by our server |
| `price` | Transaction amount / price |
| `rc` | Transaction response code |
| `balance` | Remaining balance |
| `sn` | Serial / reference number (available on successful transactions) |
| `message` | Transaction status message |

Full list of `rc` values: [Response codes (RC)](transaksi-direct/kode-respons.md).

## Callback response / acknowledgement

The callback recipient may return an HTTP response as a sign that the callback request has been received.

**Example:**

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "status": "success"
}
```

This acknowledgement is **not** used to trigger further processing.

## Retry policy

Callbacks do not implement an automatic retry mechanism.

If callback delivery fails due to a timeout, network disruption, or an unsuccessful HTTP response, the callback will not be resent automatically by the system.

If needed, the callback notification can be resent manually from the system.

If the final transaction status has not been received, use the Check Status API (`POST /status`) with the same `request_id` to get the latest transaction status.
