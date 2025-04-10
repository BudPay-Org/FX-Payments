# Fetch Transaction Statement

## Endpoint Details
- **URL:** `https://partners.budpay.com/api/v3/statement/get`
- **Method:** POST
- **Authentication:** Bearer Token

## Request Payload

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| `startDate` | String | Yes | Start date for transaction statement retrieval (YYYY-MM-DD format) |
| `endDate` | String | Yes | End date for transaction statement retrieval (YYYY-MM-DD format) |
| `currency` | String | Yes | Filter transactions by specific currency (e.g., "USD", "NGN") |


## Example Request
```bash
curl -X POST https://partners.budpay.com/api/v3/statement/get \
-H "Authorization: Bearer YOUR_SECRET_KEY" \
-H "Content-Type: application/json" \
-d '{
    "startDate": "2025-01-01",
    "endDate": "2025-01-31",
    "currency": "USD"
}'
```

## Request Headers
- `Authorization`: Bearer token (YOUR_SECRET_KEY)

## Request Payload Example
```json
{
    "startDate": "2025-01-01",
    "endDate": "2025-01-31",
    "currency": "USD"
}
```

## Successful Response (200 OK)
```json
{
  "message": "Successful",
  "status": true,
  "data": {
    "openingAvailableBalance": "3925364415.99",
    "closingAvailableBalance": "4318405260.75",
    "walletStatements": [
      {
        "transactionDate": "2024-10-15T00:01:18Z",
        "currency": "NGN",
        "note": "Walter Ledbetter|AKWUOLE OSINACHI CAMILA|R75288521048",
        "amount": "499999.5",
        "balBefore": "3925364415.99",
        "balAfter": "3924864416.49",
        "reference": "R75288521048",
        "status": "success",
        "type": "payout",
        "debitCreditIndicator": "Debit"
      },
      {
        "transactionDate": "2024-10-15T00:01:27Z",
        "currency": "NGN",
        "note": "brian tyler|UKEGBU EMMANUEL UKACHUKWU|R81417442898",
        "amount": "247500",
        "balBefore": "3924864416.49",
        "balAfter": "3924616916.49",
        "reference": "R81417442898",
        "status": "success",
        "type": "payout",
        "debitCreditIndicator": "Debit"
      },
      {
        "transactionDate": "2024-10-15T00:01:48Z",
        "currency": "NGN",
        "note": "Ihebuche Okorie|NWANKWO KINGSLEY CHUKWUEMEKA|R27480485026",
        "amount": "250800",
        "balBefore": "3924616916.49",
        "balAfter": "3924366116.49",
        "reference": "R27480485026",
        "status": "success",
        "type": "payout",
        "debitCreditIndicator": "Debit"
      },
      {
        "transactionDate": "2024-10-15T00:01:54Z",
        "currency": "NGN",
        "note": "Malkia Zimbi|NAZIRU  YAKUBU|R70437007050",
        "amount": "49500",
        "balBefore": "3924366116.49",
        "balAfter": "3924316616.49",
        "reference": "R70437007050",
        "status": "success",
        "type": "payout",
        "debitCreditIndicator": "Debit"
      }
    ]
  }
}
```

### Response Fields
| Field | Type | Description | Nullable |
|-------|------|-------------|----------|
| `message` | String | Response status message | No |
| `status` | Boolean | Indicates successful request | No |
| `data.openingAvailableBalance` | String | Opening balance for the period | No |
| `data.closingAvailableBalance` | String | Closing balance for the period | No |
| `data.walletStatements` | Array | List of transaction statements | No |
| `walletStatements[].transactionDate` | DateTime | Timestamp of transaction | No |
| `walletStatements[].currency` | String | Transaction currency | No |
| `walletStatements[].note` | String | Transaction description | No |
| `walletStatements[].amount` | String | Transaction amount | No |
| `walletStatements[].balBefore` | String | Balance before transaction | No |
| `walletStatements[].balAfter` | String | Balance after transaction | No |
| `walletStatements[].reference` | String | Transaction reference | No |
| `walletStatements[].status` | String | Transaction status | No |
| `walletStatements[].type` | String | Transaction type | No |
| `walletStatements[].debitCreditIndicator` | String | Indicates if transaction is debit or credit | No |


## Error Responses

### Unauthorized (401)
```json
{
    "message": "Invalid Merchant Authorization",
    "status": false,
    "error": "Authentication failed"
}
```

### Not Found (404)
```json
{
    "message": "No record found for the Business",
    "status": false,
    "error": "Business not found"
}
```

```json
{
    "message": "No record found for selected period",
    "status": false,
    "error": "No transactions found"
}
```

### Bad Request (400)
```json
{
    "message": "Invalid date range",
    "status": false,
    "error": "Start date must be before end date"
}
```

### Server Error (500)
```json
{
    "message": "Internal Server Error",
    "status": false,
    "error": "Unable to retrieve transaction statement"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 404 | No record found for the Business | Business account does not exist |
| 404 | No record found for selected period | No transactions found in date range |
| 400 | Invalid date range | Start date is after end date |
| 500 | Internal Server Error | Server encountered an error |


## Notes
- Dates must be in YYYY-MM-DD format
- `currency` parameter is optional and can be used to filter transactions
- Requires valid authentication token