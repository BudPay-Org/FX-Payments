# Vendor Payment FX Transfer API Documentation

## Overview
The FX Transfer API enables you to initiate cross-currency vendor payments using a previously obtained rate token. This endpoint processes international transfers based on the exchange rate locked in by your rate token.

## Endpoint
```
POST https://partners.budpay.com/api/v3/vendorpayment/fx-transfer
```

## Authentication
Authentication is required for this endpoint. Use your Secret Key in the Authorization header.

## Headers
| Header | Value | Description |
|--------|-------|-------------|
| Authorization | {{SecretKey}} | Your API secret key |
| Content-Type | application/json | Indicates that the request body is in JSON format |

## Request Parameters
The request body should be a JSON object with the following parameters:

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| amount | Number | Yes | Amount to transfer in target currency | `100` |
| bankCountry | String | Yes | ISO 3166-1 alpha-2 country code of recipient bank | `"GB"` |
| phone | String | Yes | Recipient's contact phone number with country code | `"447032522089"` |
| email | String | Yes | Recipient's email address | `"pe@budpay.com"` |
| bankName | String | Yes | Full name of the recipient's bank | `"Citibank NA"` |
| accountNumber | String | Yes | Account number or IBAN of recipient | `"GB50CITI185008133062560"` |
| accountName | String | Yes | Name on the recipient's account | `"BudPay"` |
| accountType | String | Yes | Type of account ("Individual" or "Corporate") | `"Corporate"` |
| bankAddress | String | Yes | Complete physical address of recipient bank | `"Canada Square, Canary Wharf, London, E14 5LB, United Kingdom"` |
| city | String | Yes | City where recipient bank is located | `"London"` |
| postalCode | String | Yes | Postal/ZIP code of recipient bank | `"E14 5LB"` |
| swiftCode | String | Yes | SWIFT/BIC code of recipient bank | `"CITIGB2LXXX"` |
| narration | String | Yes | Description or purpose of transfer | `"Test"` |
| currency | String | Yes | ISO 4217 currency code for transfer | `"USD"` |
| reference | String | Yes | Unique identifier for this transaction | `"202504041256009"` |


## Example Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/fx-transfer' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "amount": 100,
  "bankCountry": "GB",
  "phone": "447032522089",
  "email": "pe@budpay.com",
  "bankName": "Citibank NA",
  "accountNumber": "GB50CITI185008133062560",
  "accountName": "BudPay",
  "accountType": "Corporate",
  "bankAddress": "Canada Square, Canary Wharf, London, E14 5LB, United Kingdom",
  "city": "London",
  "postalCode": "E14 5LB",
  "swiftCode": "CITIGB2LXXX",
  "narration": "Test",
   "currency": "USD",
  "reference": "202504041256009"
}'
```


## Example Response
```json
{
    "success": true,
    "message": "Transfer successfully logged and processing",
    "data": {
        "status": "pending",
        "currency": "USD",
        "amount": 100.00,
        "bankCountry": "GB",
        "bankName": "Citibank NA",
        "accountNumber": "GB50CITI185008133062560",
        "accountName": "BudPay",
        "swiftCode": "CITIGB2LXXX",
        "narration": "Test",
        "reference": "202504041256009",
        "domain": "test",
        "createdAt": "2025-04-04T00:49:21.7035798Z",
        "updatedAt": "2025-04-04T00:49:21.7035798Z"
    }
}
```

## Response Parameters
| Field | Type | Description | Nullable |
|-------|------|-------------|----------|
| success | Boolean | Indicates if the request was successful | No |
| message | String | Status message for the operation | No |
| data | Object | Contains the transfer details | No |
| data.status | String | Current status of the transfer (e.g., "pending") | No |
| data.currency | String | Currency code of the transfer (e.g., "USD") | No |
| data.amount | Number | Transfer amount in specified currency | No |
| data.bankCountry | String | ISO country code of recipient bank | No |
| data.bankName | String | Name of the recipient bank | No |
| data.accountNumber | String | Recipient's account number or IBAN | No |
| data.accountName | String | Name of the account holder | No |
| data.swiftCode | String | SWIFT/BIC code of recipient bank | No |
| data.narration | String | Transfer description/note | No |
| data.reference | String | Unique transaction reference | No |
| data.domain | String | API environment ("test" or "live") | No |
| data.createdAt | String | ISO 8601 timestamp of creation | No |
| data.updatedAt | String | ISO 8601 timestamp of last update | No |


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
    "message": "One or more required fields is missing"
}
```

```json
{
    "status": false,
    "message": "Reference already exists"
}
```

```json
{
    "status": false,
    "message": "Insufficient balance for payment processing"
}
```

### 403 Forbidden
```json
{
    "status": false,
    "message": "Incomplete merchant setup please contact admin"
}
```

### 503 Service Unavailable
```json
{
    "status": false,
    "message": "Service Unavailable, please contact support"
}
```

### 500 Internal Server Error
```json
{
    "status": false,
    "message": "Unable to process FX transfer"
}
```

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
| 400 | One or more required fields is missing | Required parameters not provided |
| 400 | Reference already exists | Duplicate transaction reference |
| 400 | Insufficient balance for payment processing | Not enough funds available |
| 403 | Incomplete merchant setup please contact admin | Account setup incomplete |
| 503 | Service Unavailable, please contact support | Service temporarily unavailable |
| 500 | Unable to process FX transfer | Failed to process the transfer |
| 500 | An error occurred initiating transfer | General server error |


## Notes
- The rateToken has a limited validity period (typically 5 minutes) as specified in the fx-rate response.
- The reference must be unique for each transaction.
- The accountType should match one of the types returned by the account-types endpoint.
- For international transfers, ensure that all bank details are accurate, including the SWIFT/BIC code.
- Currency codes should be provided in the ISO 4217 format.
- Country codes should be provided in the ISO 3166-1 alpha-2 format.