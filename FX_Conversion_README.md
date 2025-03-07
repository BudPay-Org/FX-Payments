# FX Conversion Endpoint Documentation

## Overview
The FX Conversion endpoint allows you to execute a currency conversion transaction using a previously obtained rate token. This endpoint finalizes the conversion process at the locked-in exchange rate.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/vendorpayment/fx-conversion`
- **Method**: POST
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)

## Request Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| rateToken | The unique token obtained from a previous FX rate request that locks in the exchange rate | Yes | string |
| reference | A unique reference identifier for this conversion transaction | Yes | string |

## Request Example

```json
{
  "rateToken": "fx_rate_token_12345abcde",
  "reference": "TRX_20250307_001"
}
```

## Response Format

### Success Response (200 OK)

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

1. This endpoint should be called after obtaining a valid `rateToken` from the FX Rate endpoint.
2. The `reference` parameter should be unique for each transaction to ensure proper tracking.
3. The exchange rate used for the conversion is the one associated with the provided `rateToken`.
4. Ensure the `rateToken` hasn't expired before making this request (check the `rateExpiry` from the FX Rate response).
5. The response will contain the status of the conversion, which may be immediate or pending depending on the system configuration.

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

## Implementation Example

```bash
# Example implementation using curl
curl -X POST "https://partners.budpay.com/api/v3/vendorpayment/fx-conversion" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "rateToken": "fx_rate_token_12345abcde",
    "reference": "TRX_20250307_001"
  }'
```
