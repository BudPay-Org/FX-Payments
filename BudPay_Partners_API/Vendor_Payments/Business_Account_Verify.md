# Vendor Payment Account Verification API Documentation

## Overview
The Account Verification API allows you to verify business account details before making vendor payments. This endpoint validates the account number against the provided bank code and returns the account holder's name.

## Endpoint
```
POST https://partners.budpay.com/api/v3/vendorpayment/business-account/verify
```

## Authentication
Authentication is required for this endpoint. Use your Secret Key in the Authorization header.

## Headers
| Header | Value | Description |
|--------|-------|-------------|
| Authorization | {{SecretKey}} | Your API secret key |
| Content-Type | application/json | Indicates that the request body is in JSON format |

## Request Parameters
The request body should be a JSON object with the following parameters:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| bank_code | String | Yes | The code of the bank (e.g., "BudPay") |
| account_number | String | Yes | The account number to verify |
| currency | String | Yes | The currency code of the account (e.g., "NGN") |

## Example Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/business-account/verify' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data '{
  "bank_code": "BudPay",
  "account_number": "16686",
  "currency": "NGN"
}'
```

## Example Response
```json
{
    "success": true,
    "message": "Account name retrieved",
    "data": "MAJORSIGNATURE94"
}
```

## Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| success | Boolean | Status of the request (true for success) |
| message | String | A description of the outcome |
| data | String | The account holder's name |

## Error Responses
If the request fails, the API will return an error response:

```json
{
  "success": false,
  "message": "Error message describing the issue",
  "code": "ERROR_CODE"
}
```

## Notes
- Currency codes should be provided in the ISO 4217 format (e.g., NGN, USD, EUR).
- The bank_code parameter should be a valid bank identifier recognized by the system.
- The account verification process helps ensure funds are sent to the correct recipient.