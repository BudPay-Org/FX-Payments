# FX Conversion Endpoint

**URL:** `https://partners.budpay.com/api/v3/vendorpayment/fx-conversion`  
**Method:** POST

## Request Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| rateToken | The unique token obtained from a previous FX rate request that locks in the exchange rate | Yes | string |
| reference | A unique reference identifier for this conversion transaction | Yes | string |

## Response Codes

### 200 OK

```json
{
  "status": "string",
  "statusMessage": "string",
  "id": 0,
  "rateToken": "string",
  "reference": "string",
  "rate": 0,
  "fromCurrency": "string",
  "toCurrency": "string",
  "fromAmount": 0,
  "toAmount": 0
}
```

| Field | Description |
|-------|-------------|
| status | The status of the conversion transaction |
| statusMessage | A human-readable message describing the status |
| id | Unique identifier for the conversion transaction |
| rateToken | The rate token used for this conversion |
| reference | The reference identifier provided in the request |
| rate | The exchange rate used for the conversion |
| fromCurrency | The source currency code |
| toCurrency | The target currency code |
| fromAmount | The amount in the source currency |
| toAmount | The amount in the target currency |

### 400 Bad Request

```json
{
  "type": "string",
  "title": "string",
  "status": 0,
  "detail": "string",
  "instance": "string",
  "additionalProp1": "string",
  "additionalProp2": "string",
  "additionalProp3": "string"
}
```

### 500 Internal Server Error

Internal Server Error
```
