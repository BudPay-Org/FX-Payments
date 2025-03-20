# Make Partial Refund Endpoint Documentation

## Overview
Initiates a partial refund for a specific transaction.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/partial-refund`
- **Method**: POST
- **Authentication**: Bearer token required

## Request Parameters

| Key            | Description                                      | Required |
|---------------|--------------------------------------------------|----------|
| reference     | The transaction reference to refund             | Yes      |
| amount        | The partial refund amount                       | Yes      |
| customer_note | A note explaining the refund for the customer   | Yes      |
| merchant_note | A note explaining the refund for the merchant   | Yes      |

## Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/partial-refund' \
  -H 'accept: text/plain' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "reference": "string",
  "amount": 50.00,
  "customer_note": "Partial refund for order #12345",
  "merchant_note": "Refund issued due to overcharge"
}'
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

### Error Response (400 Bad Request)
```json
{
  "status": false,
  "message": "no record found for transaction with reference string"
}
```

## Usage Notes
- Ensure the transaction reference provided exists before making a refund request.
- The `amount` field should be less than or equal to the total transaction amount.
- Refund status can be `pending`, `processed`, or `failed` depending on the request processing stage.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```