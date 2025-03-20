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
curl -X GET 'https://partners.budpay.com/api/v3/refund/ffddf' \
  -H 'accept: text/plain' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
  "status": true,
  "data": {
    "id": 0,
    "refundReference": "string",
    "amount": "string",
    "currency": "string",
    "domain": "string",
    "initiatedBy": "string",
    "channel": "string",
    "merchantNote": "string",
    "customerNote": "string",
    "status": "processed",
    "transactionReference": "string",
    "createdAt": "string"
  }
}
```

| Key                 | Description                                         |
|---------------------|-----------------------------------------------------|
| status             | Indicates if the request was successful             |
| data               | Object containing refund details                     |
| id                 | Unique refund identifier                            |
| refundReference    | Unique reference for the refund                     |
| amount             | Refund amount                                       |
| currency           | Currency of the refund                              |
| domain            | API environment (`live` or `sandbox`)                |
| initiatedBy        | Who initiated the refund (`system`, `merchant`, etc.) |
| channel            | Refund channel (e.g., `wema`, `pwbt`)               |
| merchantNote       | Merchant's note explaining the refund               |
| customerNote       | Customer-facing note for the refund                 |
| status             | Refund status (`pending`, `processed`, `failed`)    |
| transactionReference | Reference of the original transaction              |
| createdAt          | Timestamp when the refund was initiated             |

### Error Response (404 Not Found)
```json
{
  "status": false,
  "message": "no record found for transaction with reference ffddf"
}
```

## Usage Notes
- Use this endpoint to track the status of a specific refund transaction.
- The `reference` parameter must match the refund reference used during the refund process.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

