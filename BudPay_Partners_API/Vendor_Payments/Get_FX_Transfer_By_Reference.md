# Get FX Transfer by Reference API Documentation

## Overview
This API endpoint allows you to retrieve the details and current status of a specific vendor payment FX transfer using its reference number. This is useful for tracking the progress of international transfers and retrieving their latest status.

## Endpoint
```
GET https://partners.budpay.com/api/v3/vendorpayment/fx-transfer/{reference}
```

## Authentication
Authentication is required for this endpoint. Use your Secret Key in the Authorization header.

## Headers
| Header | Value | Description |
|--------|-------|-------------|
| Authorization | {{SecretKey}} | Your API secret key |

## Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| reference | String | Yes | The unique reference of the transfer you want to retrieve |

## Example Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/vendorpayment/fx-transfer/202504041256005' \
--header 'Authorization: {{SecretKey}}'
```

## Example Response
```json
{
    "success": true,
    "message": "Transfer successfully logged and processing",
    "data": {
        "status": "awaiting approval",
        "fromCurrency": "NGN",
        "toCurrency": "USD",
        "buyAmount": 2.00,
        "sellAmount": 3000.00,
        "bankCountry": "GB",
        "bankName": "Citibank NA",
        "accountNumber": "GB50CITI185008133062560",
        "accountName": "BudPay",
        "swiftCode": "CITIGB2LXXX",
        "narration": "Test",
        "reference": "202504041256005",
        "domain": "test",
        "createdAt": "2025-04-04T00:49:22",
        "updatedAt": "2025-04-04T00:49:37"
    }
}
```

## Response Parameters
| Parameter | Type | Description | Nullable |
|-----------|------|-------------|----------|
| success | Boolean | Status of the request (true for success) | No |
| message | String | A description of the outcome | No |
| data.status | String | Current status of the transfer (e.g., "awaiting approval", "pending", "completed", "failed") | No |
| data.fromCurrency | String | The source currency code | No |
| data.toCurrency | String | The target currency code | No |
| data.buyAmount | Number | The amount in the target currency | No |
| data.sellAmount | Number | The amount in the source currency | No |
| data.bankCountry | String | ISO country code of the recipient bank | No |
| data.bankName | String | Name of the recipient bank | No |


## Error Responses

### 401 Unauthorized
```json
{
    "success": false,
    "message": "Invalid Merchant Authorization"
}
```

### 400 Bad Request
```json
{
    "success": false,
    "message": "Please supply the reference"
}
```

### 404 Not Found
```json
{
    "success": false,
    "message": "Reference does not exists"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 400 | Please supply the reference | Reference parameter is missing |
| 404 | Reference does not exists | No transfer found with provided reference |