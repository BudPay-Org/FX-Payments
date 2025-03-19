# FX Rate Endpoint Documentation

## Overview
The FX Rate endpoint provides currency conversion rates between two specified currencies and can be used to calculate equivalent amounts in either the source or target currency.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/vendorpayment/fx-rate`
- **Method**: POST
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)

## Request Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| fromCurrency | The source currency code (e.g., "USD", "EUR", "NGN") | Yes | string |
| toCurrency | The target currency code for the conversion | Yes | string |
| fromAmount | The amount in the source currency to be converted | No* | number |
| toAmount | The amount in the target currency | No* | number |

*Note: Either `fromAmount` OR `toAmount` should be provided, but not necessarily both.

## Request Example

```json
{
  "fromCurrency": "USD",
  "toCurrency": "NGN",
  "fromAmount": 100
}
```

## Response Format

### Success Response (200 OK)

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

### Error Response (400 Bad Request)

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

### Error Response (500 Internal Server Error)

Internal Server Error

## Usage Notes

1. The rate provided by this endpoint has an expiration time, indicated by both the `rateExpiry` timestamp and the `rateValidityInSeconds` value.
2. The `rateToken` can be used in subsequent API calls to lock in the exchange rate for a transaction.
3. You can calculate either way:
   - Provide `fromAmount` to get the equivalent `toAmount`
   - Provide `toAmount` to get the equivalent `fromAmount`

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

## Implementation Example

```bash
# Example implementation using curl
curl -X POST "https://partners.budpay.com/api/v3/vendorpayment/fx-rate" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "fromCurrency": "USD",
    "toCurrency": "NGN",
    "fromAmount": 100
  }'
```
