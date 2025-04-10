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

| Key           | Description                                     | Nullable |
|--------------|-------------------------------------------------|----------|
| success      | Indicates if the request was successful         | No       |
| message      | Status message                                  | No       |
| data         | Object containing transfer details              | No       |
| id           | Unique transfer identifier                      | No       |
| reference    | Transaction reference ID                        | No       |
| currency     | Currency of the transfer                        | No       |
| amount       | Transfer amount                                 | No       |
| fee          | Transaction fee                                 | No       |
| bank_code    | Recipient's bank code                          | No       |
| bank_name    | Recipient's bank name                          | No       |
| account_number | Recipient's account number                    | No       |
| account_name  | Recipient's account name                      | No       |
| narration    | Transfer description                           | No       |
| domain       | API environment (`live` or `sandbox`)          | No       |
| status       | Transfer status (`pending`, `completed`, etc.) | No       |
| updated_at   | Last updated timestamp                         | No       |
| created_at   | Timestamp of transfer creation                 | No       |


### Error Responses

#### 401 Unauthorized
```json
{
    "status": false,
    "message": "Invalid Merchant Authorization"
}
```

#### 400 Bad Request
```json
{
    "status": false,
    "message": "One or more required fields is missing"
}
```

```json
{
    "status": false,
    "message": "Transaction Amount must be greater than 0"
}
```

```json
{
    "status": false,
    "message": "Unknown bank code, bank code must be 6 digits"
}
```

```json
{
    "status": false,
    "message": "MetaData must be a valid JSON string"
}
```

```json
{
    "status": false,
    "message": "Transaction reference already exist"
}
```

```json
{
    "status": false,
    "message": "You have insufficient balance"
}
```

#### 403 Forbidden
```json
{
    "status": false,
    "message": "Incomplete merchant setup please contact admin"
}
```

#### 503 Service Unavailable
```json
{
    "status": false,
    "message": "Service Unavailable, please contact support"
}
```

#### 500 Internal Server Error
```json
{
    "status": false,
    "message": "An error occurred initiating transfer"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 400 | One or more required fields is missing | Required request parameters are not provided |
| 400 | Transaction Amount must be greater than 0 | Invalid amount specified |
| 400 | Unknown bank code, bank code must be 6 digits | Invalid bank code format |
| 400 | MetaData must be a valid JSON string | Invalid metadata format |
| 400 | Transaction reference already exist | Duplicate reference ID |
| 400 | You have insufficient balance | Not enough funds to complete transfer |
| 403 | Incomplete merchant setup please contact admin | Account setup needs completion |
| 503 | Service Unavailable, please contact support | Service temporarily unavailable |
| 500 | An error occurred initiating transfer | Server encountered an error |

## Usage Notes
- Ensure the bank code is obtained from the **Get Payout Banks** endpoint.
- The `reference` field must be unique for each transfer.
- IP whitelisting may be required to use this endpoint.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

