# FX Rate Endpoint

**URL:** `https://partners.budpay.com/api/v3/vendorpayment/fx-rate`  
**Method:** POST

## Request Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| fromCurrency | The source currency code (e.g., "USD", "EUR", "NGN") | Yes | string |
| toCurrency | The target currency code for the conversion | Yes | string |
| fromAmount | The amount in the source currency to be converted | No* | number |
| toAmount | The amount in the target currency | No* | number |

*Note: Either `fromAmount` OR `toAmount` should be provided, but not necessarily both.

## Response Codes

### 200 OK

```json
{
  "rateToken": "string",
  "rate": 0,
  "rateExpiry": "2025-03-06T21:41:15.757Z",
  "rateValidityInSeconds": 0,
  "fromCurrency": "string",
  "toCurrency": "string",
  "fromAmount": 0,
  "toAmount": 0
}
```

| Field | Description |
|-------|-------------|
| rateToken | A unique token that can be used to lock in this exchange rate |
| rate | The exchange rate between the two currencies |
| rateExpiry | ISO 8601 timestamp indicating when the rate will expire |
| rateValidityInSeconds | The number of seconds the rate remains valid |
| fromCurrency | The source currency code used in the request |
| toCurrency | The target currency code used in the request |
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
