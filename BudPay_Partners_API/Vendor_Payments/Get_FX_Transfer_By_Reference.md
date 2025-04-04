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
| Parameter | Type | Description |
|-----------|------|-------------|
| success | Boolean | Status of the request (true for success) |
| message | String | A description of the outcome |
| data.status | String | Current status of the transfer (e.g., "awaiting approval", "pending", "completed", "failed") |
| data.fromCurrency | String | The source currency code |
| data.toCurrency | String | The target currency code |
| data.buyAmount | Number | The amount in the target currency |
| data.sellAmount | Number | The amount in the source currency |
| data.bankCountry | String | ISO country code of the recipient bank |
| data.bankName | String | Name of the rec