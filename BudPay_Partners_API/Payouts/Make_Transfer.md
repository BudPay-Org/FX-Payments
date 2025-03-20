# Make Transfer Endpoint Documentation

## Overview
Initiates a bank transfer to a specified recipient.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/transfer`
- **Method**: POST
- **Authentication**: Bearer token required

## Request Parameters

| Key          | Description                                       | Required |
|-------------|---------------------------------------------------|----------|
| currency    | The currency code (e.g., NGN, USD)               | Yes      |
| amount      | The amount to be transferred                     | Yes      |
| bank_code   | The recipient's bank code                        | Yes      |
| account_number | The recipient's account number               | Yes      |
| account_name  | The recipient's account name                   | Yes      |
| narration   | Transfer description or purpose                  | Yes      |
| reference   | Unique reference ID for the transaction          | Yes      |
| meta_data   | JSON-formatted metadata for additional details   | No       |

## Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/transfer' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "currency": "NGN",
    "amount": "100",
    "bank_code": "000013",
    "account_number": "0004498921",
    "account_name": "OLUWAFEMI AZEEZ OLUWASEUN",
    "narration": "Azed transfer",
    "reference": "AZEDPY0000015",
    "meta_data": "{\"sender_name\" : \"Azeez Oluwafemi\",\"sender_address\" : \"No 18 BUD Infrastructure BLVD Lekki Lagos Nigeria\"}"
  }'
```

## Response Format

### Success Response (200 OK)
```json
{
  "success": true,
  "message": "Transfer successfully logged and Processing",
  "data": {
    "id": "85635",
    "reference": "AZEDPY0000016",
    "currency": "NGN",
    "amount": "100",
    "fee": "10",
    "bank_code": "000013",
    "bank_name": "GUARANTY TRUST BANK",
    "account_number": "0004498921",
    "account_name": "OLUWAFEMI AZEEZ OLUWASEUN",
    "narration": "Azed transfer",
    "domain": "live",
    "status": "pending",
    "updated_at": "2023-04-01T10:27:08.2274922",
    "created_at": "2023-04-01T10:27:08.2274922"
  }
}
```

| Key           | Description                                     |
|--------------|-------------------------------------------------|
| success      | Indicates if the request was successful        |
| message      | Status message                                 |
| data         | Object containing transfer details            |
| id           | Unique transfer identifier                    |
| reference    | Transaction reference ID                      |
| currency     | Currency of the transfer                      |
| amount       | Transfer amount                               |
| fee          | Transaction fee                               |
| bank_code    | Recipient's bank code                         |
| bank_name    | Recipient's bank name                         |
| account_number | Recipient's account number                 |
| account_name  | Recipient's account name                     |
| narration    | Transfer description                          |
| domain       | API environment (`live` or `sandbox`)        |
| status       | Transfer status (`pending`, `completed`, etc.) |
| updated_at   | Last updated timestamp                        |
| created_at   | Timestamp of transfer creation               |

### Error Response (401 Unauthorized)
```json
{
  "status": false,
  "message": "IP whitelisting is required to access this service."
}
```

## Usage Notes
- Ensure the bank code is obtained from the **Get Payout Banks** endpoint.
- The `reference` field must be unique for each transfer.
- IP whitelisting may be required to use this endpoint.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

