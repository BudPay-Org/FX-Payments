# Get Refund by Reference Endpoint Documentation

## Overview
Retrieves details of a specific refund using the refund reference.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/refund/{reference}`
- **Method**: GET
- **Authentication**: Bearer token required

## Path Parameters

| Key       | Description                                      | Required |
|-----------|--------------------------------------------------|----------|
| reference | The unique refund reference to retrieve details | Yes      |

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/refund/Zotapay_6775575344' \
  -H 'accept: text/plain' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
    "status": true,
    "message": "refund data retrieved forZotapay_6775575344",
    "data": {
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
}
```

### Response Fields
| Key                 | Description                                         | Nullable |
|---------------------|-----------------------------------------------------|----------|
| status             | Indicates if the request was successful             | No       |
| data               | Object containing refund details                     | No       |
| id                 | Unique refund identifier                            | No       |
| reference          | Original transaction reference                      | No       |
| refundReference    | Unique reference for the refund                     | No       |
| amount             | Refund amount                                       | No       |
| currency           | Currency of the refund                              | No       |
| domain            | API environment (`live` or `sandbox`)                | No       |
| initiatedBy        | Who initiated the refund (`system`, `merchant`, etc.) | No       |
| channel            | Refund channel (e.g., `wema`, `pwbt`)               | No       |
| merchantNote       | Merchant's note explaining the refund               | Yes      |
| customerNote       | Customer-facing note for the refund                 | Yes      |
| status             | Refund status (`new`, `pending`, `awaiting approval`, `success`, `failed`)    | No       |
| transactionReference | Reference of the original transaction              | No       |
| createdAt          | Timestamp when the refund was initiated             | No       |


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
- Use this endpoint to track the status of a specific refund transaction.
- The `reference` parameter must match the refund reference used during the refund process.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

