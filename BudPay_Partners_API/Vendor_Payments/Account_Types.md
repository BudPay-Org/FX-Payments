# Vendor Payment Account Types API Documentation

## Overview
The Account Types API allows you to retrieve the available account types for vendor payments. This endpoint returns the list of possible account types that can be used in other Vendor Payment API calls.

## Endpoint
```
GET https://partners.budpay.com/api/v3/vendorpayment/account-types
```

## Authentication
Authentication is required for this endpoint. Use your Secret Key in the Authorization header.

## Headers
| Header | Value | Description |
|--------|-------|-------------|
| Authorization | {{SecretKey}} | Your API secret key |

## Example Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/vendorpayment/account-types' \
--header 'Authorization: {{SecretKey}}'
```

## Example Response
```json
{
    "success": true,
    "message": "Successful",
    "data": [
        {
            "id": 1,
            "name": "Individual"
        },
        {
            "id": 2,
            "name": "Corporate"
        }
    ]
}
```

## Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| success | Boolean | Status of the request (true for success) |
| message | String | A description of the outcome |
| data | Array | List of available account types |
| data[].id | Number | Unique identifier for the account type |
| data[].name | String | Name of the account type |


## Error Responses

#### 401 Unauthorized
```json
{
    "success": false,
    "message": "Invalid Merchant Authorization",
    "code": "UNAUTHORIZED"
}
```

#### 500 Internal Server Error
```json
{
    "success": false,
    "message": "An internal error occurred please try again",
    "code": "INTERNAL_ERROR"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 500 | An internal error occurred please try again | Server encountered an error processing the request |


## Notes
- The account type IDs should be used when creating or updating vendor payment configurations.
- Currently, two account types are supported: Individual (id: 1) and Corporate (id: 2).
- This endpoint does not require a request body.