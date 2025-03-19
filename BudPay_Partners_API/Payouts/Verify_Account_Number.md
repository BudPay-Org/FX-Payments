# Verify Account Number Endpoint Documentation

## Overview
Verifies a bank account number and retrieves the account holder's name.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/banks/account/verify`
- **Method**: POST
- **Authentication**: Bearer token required

## Request Parameters

| Key             | Description                                   | Required |
|----------------|-----------------------------------------------|----------|
| bank_code      | Unique code identifying the bank             | Yes      |
| account_number | The account number to verify                 | Yes      |
| currency       | Currency code (e.g., NGN for Nigerian Naira) | Yes      |

## Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/banks/account/verify' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "bank_code": "000008",
  "account_number": "1130654765",
  "currency": "NGN"
}'
```

## Response Format

### Success Response (200 OK)
```json
{
  "success": true,
  "message": "Account name retrieved",
  "data": "JOHN DOE"
}
```

| Key       | Description                                  |
|-----------|----------------------------------------------|
| success   | Indicates if the request was successful    |
| message   | Status message                              |
| data      | Retrieved account holder's name            |

### Error Response (400 Bad Request)
```json
{
  "success": false,
  "message": "Invalid bank code or account number"
}
```

### Error Response (500 Internal Server Error)
```json
{
  "success": false,
  "message": "Internal server error"
}
```

## Usage Notes
- Ensure that the bank code is obtained from the **Get Payout Banks** endpoint.
- The account number must be valid for successful verification.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

