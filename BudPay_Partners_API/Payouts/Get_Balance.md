# Get Balance Endpoint Documentation

## Overview
Retrieves the available balance for a specific currency.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/balance/{currency}`
- **Method**: GET
- **Authentication**: Bearer token required

## Path Parameters

| Key      | Description                         | Required |
|----------|-------------------------------------|----------|
| currency | The currency code (e.g., NGN, USD) | Yes      |

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/balance/NGN' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
  "success": true,
  "message": "Balance Fetched Successfully",
  "data": {
    "currency": "NGN",
    "balance": "982.45"
  }
}
```

| Key       | Description                           |
|-----------|---------------------------------------|
| success   | Indicates if the request was successful |
| message   | Status message                         |
| data      | Object containing balance details     |
| currency  | Currency of the balance               |
| balance   | Available balance in the specified currency |

### Error Response

#### 401 Unauthorized
```json
{
    "success": false,
    "message": "Invalid Merchant Authorization"
}
```

#### 404 Not Found
```json
{
    "success": false,
    "message": "Balance information not found"
}
```

#### 500 Internal Server Error
```json
{
    "success": false,
    "message": "An error occurred in GetWalletBalance"
}
```

## Usage Notes
- Use this endpoint to check the available balance in your BudPay account.
- Ensure the correct currency code is used in the request.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

