# Make Refund Endpoint Documentation

## Overview
Initiates a refund for a specific transaction.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/refund`
- **Method**: POST
- **Authentication**: Bearer token required

## Request Parameters

| Key            | Description                                      | Required |
|---------------|--------------------------------------------------|----------|
| reference     | The transaction reference to refund             | Yes      |
| customer_note | A note explaining the refund for the customer   | Yes      |
| merchant_note | A note explaining the refund for the merchant   | Yes      |

## Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/refund' \
  -H 'accept: text/plain' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "reference": "Zotapay_6775575344",
  "customer_note": "",
  "merchant_note": ""
}'
```

## Response Format

### Success Response (200 OK)
```json
{
    "status": true,
    "message": "Refund submitted and in progress ",
    "data": {
        "id": 41169,
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

### Error Response (400 Bad Request)
```json
{
  "status": false,
  "message": "no record found for transaction with reference string"
}
```

## Usage Notes
- Ensure the transaction reference provided exists before making a refund request.
- The `customer_note` and `merchant_note` provide additional context for the refund.
- Refund status can be `pending`, `processed`, or `failed` depending on the request processing stage.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

