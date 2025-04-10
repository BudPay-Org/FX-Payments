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

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

---

## Implementation Example

```bash
# Example implementation using curl
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

Where:
- `YOUR_API_KEY` should be replaced with your actual API key

---

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


## Error Responses

### 401 Unauthorized
```json
{
    "status": false,
    "message": "Invalid Merchant Authorization"
}
```

### 503 Service Unavailable
```json
{
    "status": false,
    "message": "Service not available"
}
```

### 500 Internal Server Error
```json
{
    "status": false,
    "message": "An error occurred Getting bank list"
}
```

## Response Status Codes

| Status Code | Message | Description |
|------------|---------|-------------|
| 200 | Available Banks retrieved | Successfully retrieved bank list |
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 503 | Service not available | Bank list service temporarily unavailable |
| 500 | An error occurred Getting bank list | Server encountered an error processing request |

## Usage Notes
1. This endpoint must be called before creating virtual accounts to obtain the necessary bank codes.
2. The response includes all banks available for virtual account creation within the BudPay system.
3. Bank availability may vary based on your account configuration and geographical restrictions.