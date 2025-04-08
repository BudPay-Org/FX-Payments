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

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| rateToken | String | Yes | The rate token obtained from the fx-rate endpoint |
| bankCountry | String | Yes | ISO country code of the recipient bank (e.g., "GB") |
| phone | String | No | Contact phone number for the recipient |
| email | String | No | Contact email for the recipient |
| bankName | String | Yes | Name of the recipient's bank |
| accountNumber | String | Yes | Account number or IBAN of the recipient |
| accountName | String | Yes | Name of the account holder |
| accountType | String | Yes | Type of account ("Individual" or "Corporate") |
| address | String | No | Physical address of the recipient |
| city | String | No | City of the recipient |
| postalCode | String | No | Postal code of the recipient |
| swiftCode | String | Yes | SWIFT/BIC code of the recipient's bank |
| narration | String | Yes | Description of the transfer |
| reference | String | Yes | Your unique reference for this transaction |

## Example Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/fx-transfer' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "rateToken": "bfxt5490QNNGAD2597N9",
  "bankCountry": "GB",
  "phone": "447032522089",
  "email": "pe@budpay.com",
  "bankName": "Citibank NA",
  "accountNumber": "GB50CITI185008133062560",
  "accountName": "BudPay",
  "accountType": "Corporate",
  "address": "Canada Square, Canary Wharf, London, E14 5LB, United Kingdom",
  "city": "London",
  "postalCode": "E14 5LB",
  "swiftCode": "CITIGB2LXXX",
  "narration": "Test",
  "reference": "202504041256005"
}'
```

## Example Response
```json
{
    "success": true,
    "message": "Transfer successfully logged and processing",
    "data": {
        "status": "pending",
        "fromCurrency": "NGN",
        "toCurrency": "USD",
        "buyAmount": 2.00,
        "sellAmount": 3000.00,
        "bankCountry": "GB",
        "bankName": "Citibank NA",
        "accountNumber": "GB50CITI185008133062560",
        "accountName": "BudPay",
        "swiftCode": "CITIGB2LXXX",
        "narration": "Test",
        "reference": "202504041256005",
        "domain": "test",
        "createdAt": "2025-04-04T00:49:21.7035798Z",
        "updatedAt": "2025-04-04T00:49:21.7035798Z"
    }
}
```

## Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| success | Boolean | Status of the request (true for success) |
| message | String | A description of the outcome |
| data.status | String | Current status of the transfer (e.g., "pending") |
| data.fromCurrency | String | The source currency code |
| data.toCurrency | String | The target currency code |
| data.buyAmount | Number | The amount in the target currency |
| data.sellAmount | Number | The amount in the source currency |
| data.bankCountry | String | ISO country code of the recipient bank |
| data.bankName | String | Name of the recipient's bank |
| data.accountNumber | String | Account number or IBAN of the recipient |
| data.accountName | String | Name of the account holder |
| data.swiftCode | String | SWIFT/BIC code of the recipient's bank |
| data.narration | String | Description of the transfer |
| data.reference | String | Your unique reference for this transaction |
| data.domain | String | Environment identifier (e.g., "test" or "live") |
| data.createdAt | String | ISO 8601 timestamp of when the transfer was created |
| data.updatedAt | String | ISO 8601 timestamp of when the transfer was last updated |

## Error Responses
If the request fails, the API will return an error response:

```json
{
  "success": false,
  "message": "Error message describing the issue",
  "code": "ERROR_CODE"
}
```

<!-- Common error codes:
- `INVALID_RATE_TOKEN`: The rate token is invalid or has expired
- `INVALID_BANK_DETAILS`: One or more of the bank details provided are invalid
- `DUPLICATE_REFERENCE`: The reference has already been used
- `INSUFFICIENT_FUNDS`: Insufficient funds to complete the transaction
- `AUTHENTICATION_ERROR`: Invalid or missing authentication credentials
- `SERVER_ERROR`: An internal server error occurred -->

## Notes
- The rateToken has a limited validity period (typically 5 minutes) as specified in the fx-rate response.
- The reference must be unique for each transaction.
- The accountType should match one of the types returned by the account-types endpoint.
- For international transfers, ensure that all bank details are accurate, including the SWIFT/BIC code.
- Currency codes should be provided in the ISO 4217 format.
- Country codes should be provided in the ISO 3166-1 alpha-2 format.