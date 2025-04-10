# Get Payout Banks Endpoint Documentation

## Overview
Retrieves a list of payout banks available in Nigeria.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/banks/ng`
- **Method**: GET
- **Authentication**: Bearer token required

## Request Parameters
This endpoint does not require any request parameters.

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/banks/{countryCode}' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
  "success": true,
  "message": "Bank list retrieved",
  "currency": "NGN",
  "data": [
    {
      "bank_name": "AB MICROFINANCE BANK",
      "bank_code": "090270"
    },
    {
      "bank_name": "HACKMAN MICROFINANCE BANK",
      "bank_code": "090147"
    }
  ]
}
```

| Key        | Description                          |
|------------|--------------------------------------|
| success    | Indicates if the request was successful |
| message    | Status message                        |
| currency   | Currency code for the bank list      |
| data       | Array of available banks             |
| bank_name  | Name of the bank                     |
| bank_code  | Unique code identifying the bank    |

### Error Response (401 Unauthorized)
```json
{
    "status": false,
    "message": "Invalid Merchant Authorization"
}
```

### Error Response (500 Internal Server Error) 
```json
{
    "status": false,
    "message": "An error occurred getting bank list"
}
```

## Usage Notes
- This endpoint returns a list of banks that support payouts in Nigeria.
- Ensure that a valid API key is included in the Authorization header.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

