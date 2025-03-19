# Virtual Account Bank List Endpoint Documentation

## Overview
This endpoint retrieves a list of available banks for virtual account creation within the BudPay system. This information is essential before creating virtual accounts as it provides the necessary bank codes needed for account setup.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list`
- **Method**: GET
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Request Parameters
This endpoint does not require any request parameters.

## Response Format

### Success Response
```json
{
  "status": true,
  "message": "Available Banks retrieved",
  "data": [
    {
      "bankCode": "000017",
      "bankName": "Wema Bank"
    },
    {
      "bankCode": "000031",
      "bankName": "Premium Trust Bank"
    }
  ]
}
```

| Field | Description |
|-------|-------------|
| status | Boolean indicating if the request was successful |
| message | A message describing the result of the operation |
| data | An array of available banks |
| data[].bankCode | The code identifying the bank |
| data[].bankName | The name of the bank |

### Error Response
```json
{
  "status": false,
  "message": "Error message"
}
```

## Usage Notes
1. This endpoint must be called before creating virtual accounts to obtain the necessary bank codes.
2. The response includes all banks available for virtual account creation within the BudPay system.
3. Bank availability may vary based on your account configuration and geographical restrictions.

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

## Implementation Example

```bash
# Example implementation using curl
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

Where:
- `YOUR_API_KEY` should be replaced with your actual API key