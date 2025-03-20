# Get Payout Details Endpoint Documentation

## Overview
Retrieves details of a specific payout transaction using the reference ID.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/transfers/{reference}`
- **Method**: GET
- **Authentication**: Bearer token required

## Path Parameters

| Key       | Description                                  | Required |
|-----------|----------------------------------------------|----------|
| reference | The unique reference ID of the payout       | Yes      |

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/transfers/AZEDPY0000016' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Response Format

### Success Response (200 OK)
```json
{
  "success": true,
  "message": "Transfer retrieved",
  "data": {
    "id": "85635",
    "sessionid": "000023230401102715005053452141",
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
    "status": "success",
    "updated_at": "2023-04-01T10:27:08",
    "created_at": "2023-04-01T10:27:08"
  }
}
```

| Key           | Description                                      |
|--------------|--------------------------------------------------|
| success      | Indicates if the request was successful         |
| message      | Status message                                  |
| data         | Object containing payout details               |
| id           | Unique transfer identifier                     |
| sessionid    | Internal session ID for tracking               |
| reference    | Transaction reference ID                       |
| currency     | Currency of the payout                         |
| amount       | Payout amount                                  |
| fee          | Transaction fee                                |
| bank_code    | Recipient's bank code                          |
| bank_name    | Recipient's bank name                          |
| account_number | Recipient's account number                  |
| account_name  | Recipient's account name                      |
| narration    | Payout description                             |
| domain       | API environment (`live` or `sandbox`)         |
| status       | Payout status (`pending`, `success`, etc.)     |
| updated_at   | Last updated timestamp                         |
| created_at   | Timestamp of payout creation                  |

### Error Response (400 Bad Request)
```json
{
  "success": false,
  "message": "Invalid reference ID"
}
```

### Error Response (404 Not Found)
```json
{
  "success": false,
  "message": "Payout details not found"
}
```

### Error Response (500 Internal Server Error)
```json
{
  "success": false,
  "message": "Internal server error"
}
```

## Usage Notes
- Use this endpoint to track the status of a specific payout transaction.
- The `reference` parameter must match the transaction reference used during the transfer.

## Authentication
Include your API key as a Bearer token in the Authorization header:
```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

