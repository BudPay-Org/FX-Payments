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
  "amount": 20,
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
        "id": 41170,
        "refundReference": "BR1904WA6G6TFYNC0YRC",
        "amount": "20",
        "currency": "KES",
        "domain": "test",
        "initiatedBy": "self",
        "channel": "API",
        "merchantNote": " refund for transaction BUD_17377402598649448",
        "customerNote": " refund for transaction BUD_17377402598649448",
        "status": "pending",
        "createdAt": "2025-04-04T02:31:48.0000000"
    }
}
```

| Key                 | Description                                         | Nullable |
|---------------------|-----------------------------------------------------|----------|
| status             | Indicates if the request was successful             | No       |
| data               | Object containing refund details                     | No       |
| id                 | Unique refund identifier                            | No       |
| refundReference    | Unique reference for the refund                     | No       |
| amount             | Refund amount                                       | No       |
| currency           | Currency of the refund                              | No       |
| domain            | API environment (`live` or `sandbox`)                | No       |
| initiatedBy        | Who initiated the refund (`system`, `merchant`, etc.) | No       |
| channel            | Refund channel (e.g., `wema`, `pwbt`)               | No       |
| merchantNote       | Merchant's note explaining the refund               | Yes      |
| customerNote       | Customer-facing note for the refund                 | Yes      |
| status             | Refund status (`pending`, `processed`, `failed`)    | No       |
| transactionReference | Reference of the original transaction              | No       |
| createdAt          | Timestamp when the refund was initiated             | No       |


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