# Get Virtual Account By Reference Documentation

## Overview
Retrieves details of a virtual account using its reference number.

## Endpoint Details
- **URL**: `/api/v3/collection/virtual-account/{reference}`
- **Method**: GET
- **Authentication**: Bearer token required

## Request Parameters
| Parameter | Type | Location | Description | Required |
|-----------|------|----------|-------------|----------|
| reference | String | URL Path | Reference ID of the virtual account | Yes |

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-account/20250404000002' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response
```json
{
    "status": true,
    "message": "Virtual account details retrieved",
    "data": {
        "accountNumber": "9191517722",
        "accountName": "John Doe",
        "bankCode": "000017",
        "bankName": "Wema Bank",
        "accountType": "reserved",
        "accountStatus": "active",
        "reference": "20250404000002",
        "expiryInMinutes": 0,
        "createdAt": "2025-04-04T00:49:22"
    }
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

### 400 Bad Request
```json
{
    "status": false,
    "message": "One or more required value is missing"
}
```

### 404 Not Found
```json
{
    "status": false,
    "message": "No virtual account found for reference"
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
    "message": "Unable to retrieve virtual account details"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 400 | One or more required value is missing | Reference parameter not provided |
| 404 | No virtual account found for reference | Invalid or non-existent reference |
| 503 | Service not available | Service temporarily unavailable |
| 500 | Unable to retrieve virtual account details | Server encountered an error |

## Notes
- The reference must be the same one used during virtual account creation
- Ensure proper URL encoding of the reference parameter
- Account details include current status and expiry information