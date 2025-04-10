# Fund Wallet Mock Test Documentation

## Overview
This endpoint simulates funding a virtual account wallet for testing purposes.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/fund-account`
- **Method**: POST
- **Authentication**: Bearer token required

## Request Parameters

| Parameter | Type | Description | Required |
|-----------|------|-------------|----------|
| amount | Number | Amount to fund the account with | Yes |
| reference | String | Unique transaction reference | Yes |
| narration | String | Description of the transaction | Yes |
| accountNumber | String | Virtual account number to fund | Yes |

## Sample Request
```json
{
  "amount": 1000,
  "reference": "2025040909051237",
  "narration": "Test fund account",
  "accountNumber": "4050910184"
}
```

## Response Format

### Success Response
```json
{
    "status": true,
    "message": "Account has been funded successfully"
}
```


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
    "message": "One or more required value is missing"
}
```

```json
{
    "status": false,
    "message": "Amount must be zero for reserved account generation"
}
```

```json
{
    "status": false,
    "message": "Account Number does not exist"
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
    "message": "Transaction with Reference already exists"
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
    "message": "Service not available"
}
```

#### 500 Internal Server Error
```json
{
    "status": false,
    "message": "Unable to fund virtual account"
}
```

```json
{
    "status": false,
    "message": "An error occurred funding account"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 400 | One or more required value is missing | Required parameters not provided |
| 400 | Amount must be zero for reserved account | Invalid amount for account type |
| 400 | Account Number does not exist | Invalid virtual account number |
| 400 | Reference already exists | Duplicate reference provided |
| 400 | Transaction with Reference already exists | Reference already used |
| 403 | Incomplete merchant setup | Account setup needs completion |
| 503 | Service not available | Service temporarily unavailable |
| 500 | Unable to fund virtual account | Failed to process funding |
| 500 | An error occurred funding account | General server error |


## Usage Notes
- This endpoint is for testing purposes only
- All amounts are processed in the smallest currency unit
- References must be unique for each transaction
- Account number must be a valid virtual account in the system