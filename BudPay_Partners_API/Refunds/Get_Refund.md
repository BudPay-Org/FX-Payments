# Get Refunds Endpoint Documentation

## Overview
Retrieves a list of refunds processed in the BudPay system.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/refund`
- **Method**: GET
- **Authentication**: Bearer token required

## Request Parameters
This endpoint does not require any request parameters.

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/refund' \
  -H 'accept: text/plain' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
    "status": true,
    "message": "refund data retrieved ",
    "data": [
        {
            "id": 41169,
            "reference": "Zotapay_6775575344",
            "refundReference": "BR1904MY6VHZOSSSP338",
            "amount": "500.00",
            "currency": "GHS",
            "domain": "test",
            "initiatedBy": "self",
            "channel": "API",
            "merchantNote": " refund for transaction Zotapay_6775575344",
            "customerNote": " refund for transaction Zotapay_6775575344",
            "status": "pending",
            "createdAt": "2025-04-04T02:20:48.0000000"
        }
    ]
}
```

| Key             | Description                                              |
|----------------|----------------------------------------------------------|
| status         | Indicates if the request was successful                  |
| message        | Status message                                           |
| data           | Array containing refund details                          |
| id             | Unique refund identifier                                 |
| reference      | Original transaction reference                           |
| refundReference | Unique reference for the refund                         |
| amount         | Refund amount                                            |
| currency       | Currency of the refund                                   |
| domain        | API environment (`live` or `sandbox`)                     |
| initiatedBy    | Who initiated the refund (e.g., system, user)            |
| channel        | Refund channel (e.g., `wema`, `pwbt`)                    |
| merchantNote   | Merchant's note explaining the refund                    |
| customerNote   | Customer-facing note for the refund                      |
| status         | Refund status (`pending`, `processed`, etc.)             |
| createdAt      | Timestamp when the refund was initiated                  |


### Error Responses

#### 401 Unauthorized
```json
{
    "status": false,
    "message": "Invalid Merchant Authorization"
}
```

#### 404 Not Found
```json
{
    "status": false,
    "message": "No refund record found for business"
}
```

#### 500 Internal Server Error
```json
{
    "status": false,
    "message": "An internal error occurred please try again"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 404 | No refund record found for business | No refunds exist for the merchant account |
| 500 | An internal error occurred please try again | Server encountered an error processing the request |


## Usage Notes
- This endpoint returns a list of refunds associated with your BudPay account.
- Refunds can have different statuses, such as `pending` or `processed`.
- Ensure a valid API key is included in the Authorization header.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

