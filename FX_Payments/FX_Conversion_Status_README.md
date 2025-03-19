# Get FX Conversion Status Endpoint Documentation

## Overview
This endpoint allows you to retrieve the current status and details of a previously initiated FX conversion transaction using its unique reference identifier.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/vendorpayment/fx-conversion/{reference}`
- **Method**: GET
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)

## Path Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| reference | The unique reference identifier for the conversion transaction to retrieve | Yes | string |

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
| status | The current status of the conversion transaction |
| statusMessage | A human-readable message describing the status |
| id | Unique identifier for the conversion transaction |
| rateToken | The rate token used for this conversion |
| reference | The reference identifier of the transaction |
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

1. This endpoint allows you to check the status of a previously initiated conversion transaction.
2. The `status` field indicates the current state of the conversion (e.g., "pending", "completed", "failed").
3. Common status values may include:
   - PENDING: Transaction is being processed
   - COMPLETED: Transaction has been successfully processed
   - FAILED: Transaction failed to process

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

## Implementation Example

```bash
# Example implementation using curl
curl -X GET "https://partners.budpay.com/api/v3/vendorpayment/fx-conversion/ABC123XYZ" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Where:
- `ABC123XYZ` is the unique reference identifier for the conversion transaction
- `YOUR_API_KEY` should be replaced with your actual API key
