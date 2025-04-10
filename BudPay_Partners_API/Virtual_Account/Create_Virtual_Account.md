# Create Virtual Account Endpoint Documentation

## Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/collection/virtual-account' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "reference": "335456uihiuh",
    "amount": 0,
    "accountType": "reserved",
    "accountName": "9191044796",
    "bankCode": "000017",
    "firstName": "Rowland",
    "lastName": "Okondor",
    "customerEmail": "rowlandokondor15@gmail.com",
    "expiryInMinutes": 0
  }'
```

## Overview
This endpoint allows you to create a new virtual account in the BudPay system. You can create either a reserved account (dedicated to a specific customer) or a checkout account (for one-time use).

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-account`
- **Method**: POST
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)


## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.


## Implementation Example

```bash
# Example implementation using curl
curl -X POST 'https://partners.budpay.com/api/v3/collection/virtual-account' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "reference": "unique_reference_123",
    "amount": 0,
    "accountType": "reserved",
    "accountName": "CUSTOMER_ACCOUNT_NAME",
    "bankCode": "000017",
    "firstName": "Customer",
    "lastName": "Name",
    "customerEmail": "customer@example.com",
    "expiryInMinutes": 0
  }'
```

Where:
- `YOUR_API_KEY` should be replaced with your actual API key
- The request body parameters should be replaced with your actual customer information


## Request Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| reference | A unique reference identifier for this virtual account | Yes | string |
| amount | The amount to be expected (0 for unlimited) | Yes | number |
| accountType | The type of virtual account to create (valid values: "reserved" or "checkout") | Yes | string |
| accountName | The name to be displayed for the account | Yes | string |
| bankCode | The code of the bank where the account will be created (obtained from bank-list endpoint) | Yes | string |
| firstName | The first name of the account owner | Yes | string |
| lastName | The last name of the account owner | Yes | string |
| customerEmail | The email address of the account owner | Yes | string |
| expiryInMinutes | The number of minutes until account expiration (0 for no expiration) | Yes | number |

## Response Format

### Success Response
```json
{
  "status": true,
  "message": "Virtual account generated",
  "data": {
    "accountNumber": "9191517722",
    "accountName": "9191044796",
    "bankCode": "000017",
    "bankName": "Wema Bank",
    "accountType": "reserved",
    "accountStatus": "active",
    "expiryInMinutes": 0
  }
}
```

| Field | Description | Nullable |
|-------|-------------|----------|
| status | Boolean indicating if the request was successful | No |
| message | A message describing the result of the operation | No |
| data | Object containing the created virtual account details | No |
| data.accountNumber | The generated virtual account number | No |
| data.accountName | The name associated with the virtual account | No |
| data.bankCode | The code of the bank where the account is created | No |
| data.bankName | The name of the bank where the account is created | No |
| data.accountType | The type of the virtual account (e.g., "reserved") | No |
| data.accountStatus | The current status of the account (e.g., "active") | No |
| data.expiryInMinutes | The number of minutes until account expiration (0 indicates no expiration) | No |


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
    "message": "One or more required value is missing"
}
```

```json
{
    "status": false,
    "message": "Invalid account types, valid values are reserved or checkout"
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
    "message": "Amount must be greater than zero for single use(checkout) account generation"
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

```json
{
    "status": false,
    "message": "Selected bank is not available"
}
```

### 503 Service Unavailable
```json
{
    "status": false,
    "message": "Service not available"
}
```

### 500 Internal Server Error
```json
{
    "status": false,
    "message": "Unable to generate virtual account"
}
```

## Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 400 | One or more required value is missing | Required parameters not provided |
| 400 | Invalid account types | Invalid accountType parameter value |
| 400 | Amount must be zero for reserved account | Invalid amount for reserved account |
| 400 | Amount must be greater than zero for checkout | Invalid amount for checkout account |
| 400 | Reference already exists | Duplicate reference provided |
| 400 | Transaction with Reference already exists | Reference already used |
| 400 | Selected bank is not available | Invalid or unavailable bank code |
| 503 | Service not available | Virtual account service temporarily unavailable |
| 500 | Unable to generate virtual account | Server error during account creation |


## Usage Notes
1. Before creating a virtual account, first retrieve the list of available banks using the bank-list endpoint.
2. The `accountType` parameter determines how the account can be used:
   - `reserved`: A dedicated account for a specific customer that can be used for multiple transactions
   - `checkout`: A one-time use account typically used for a single transaction
3. When `expiryInMinutes` is set to 0, the account does not expire.
4. The `amount` parameter can be set to 0 for unlimited transactions or a specific amount for a single expected transaction.
5. The `reference` should be unique for each account creation request.