# Fetch Transaction Statement

## Endpoint Details
- **URL:** `https://api.budpay.com/api/v1/get-statement`
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
curl -X POST https://api.budpay.com/api/v1/get-statement \
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
    "data": [
        {
            "id": 26716266,
            "transactionDate": "2025-01-20T01:31:09Z",
            "businessId": 30,
            "currency": "USD",
            "note": "Daily settlement on 2025-01-20 with settlement batchID 2343432",
            "amount": "1",
            "balBefore": "9",
            "balAfter": "10",
            "reference": "23432432"
        }
        // ... additional transaction entries
    ]
}
```

### Response Fields
| Field | Type | Description |
|-------|------|-------------|
| `message` | String | Response status message |
| `status` | Boolean | Indicates successful request |
| `data` | Array | List of transaction statements |
| `data[].id` | Number | Unique transaction identifier |
| `data[].transactionDate` | Datetime | Timestamp of transaction |
| `data[].businessId` | Number | Associated business ID |
| `data[].currency` | String | Transaction currency |
| `data[].note` | String | Transaction description/note |
| `data[].amount` | String | Transaction amount |
| `data[].balBefore` | String | Account balance before transaction |
| `data[].balAfter` | String | Account balance after transaction |
| `data[].reference` | String | Transaction reference number |

## Error Responses

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

## Notes
- Dates must be in YYYY-MM-DD format
- `currency` parameter is optional and can be used to filter transactions
- Requires valid authentication token