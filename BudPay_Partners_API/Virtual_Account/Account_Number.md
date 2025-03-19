# Get Virtual Account Details Endpoint Documentation

## Overview
This endpoint retrieves detailed information about a specific virtual account using the account number. It provides comprehensive details including the account name, bank information, account type, status, and expiry information.

## Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-accounts/{accountNumber}`
- **Method**: GET
- **Authentication**: Bearer token authentication required (API key should be included in the Authorization header)

## Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/2041431102' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

## Path Parameters

| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| accountNumber | The virtual account number to retrieve details for | Yes | string |

## Response Format

### Success Response
```json
{
  "status": true,
  "message": "Virtual Account List Retrieved",
  "data": [
    {
      "accountNumber": "2041431102",
      "accountName": "BUDPAY/John Doe",
      "bankCode": "000031",
      "bankName": "Premium Trust Bank",
      "accountType": "reserved",
      "accountStatus": "active",
      "expiryInMinutes": 0
    }
  ]
}
```

| Field | Description |
|-------|-------------|
| status | Boolean indicating if the request was successful |
| message | A message describing the result of the operation |
| data | An array containing the virtual account details |
| data[].accountNumber | The virtual account number |
| data[].accountName | The name associated with the virtual account |
| data[].bankCode | The code of the bank where the account is created |
| data[].bankName | The name of the bank where the account is created |
| data[].accountType | The type of the virtual account (e.g., "reserved") |
| data[].accountStatus | The current status of the account (e.g., "active") |
| data[].expiryInMinutes | The number of minutes until account expiration (0 indicates no expiration) |

### Error Response
```json
{
  "status": false,
  "message": "Error message"
}
```

## Usage Notes
1. Use this endpoint to verify the details of a specific virtual account.
2. The account status field indicates whether the account is active and can receive payments.
3. An expiryInMinutes value of 0 typically indicates a permanent account with no expiration.
4. The accountType "reserved" indicates a dedicated account for a specific customer.

## Authentication
This endpoint requires authentication using a Bearer token (API key) in the Authorization header of the request.

## Implementation Example

```bash
# Example implementation using curl
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/2041431102' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

Where:
- `2041431102` is the account number you want to retrieve details for
- `YOUR_API_KEY` should be replaced with your actual API key