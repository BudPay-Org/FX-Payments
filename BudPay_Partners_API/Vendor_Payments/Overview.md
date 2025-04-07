# Vendor Payment API Overview

## Introduction

The BudPay Vendor Payment API suite provides a comprehensive set of endpoints for managing cross-border and cross-currency payments to vendors. This suite enables businesses to verify account details, retrieve exchange rates, execute currency conversions, and transfer funds internationally with real-time status updates.

## Key Features

- **Account Management**: Verify business accounts and retrieve available account types
- **Foreign Exchange Operations**: Get real-time exchange rates and execute currency conversions
- **International Transfers**: Process cross-currency vendor payments globally
- **Internal Transfers**: Move funds between merchants within the platform
- **Real-time Notifications**: Receive webhooks for transaction status updates

## Authentication

All API requests require authentication using your Secret Key in the Authorization header:

```
Authorization: {{SecretKey}}
```

## Core API Endpoints

### Account Management

#### [Account Types](./Account_Types.md)
Retrieve available account types (Individual/Corporate) for vendor payments.
```
GET /api/v3/vendorpayment/account-types
```

#### [Business Account Verification](./Business_Account_Verify.md)
Verify business account details before making vendor payments.
```
POST /api/v3/vendorpayment/business-account/verify
```

### Foreign Exchange Operations

#### [FX Rate](./FX_Rate.md)
Get exchange rates between two currencies and calculate equivalent amounts.
```
POST /api/v3/vendorpayment/fx-rate
```

#### [FX Conversion](./FX_Conversion_01.md)
Execute a currency conversion transaction using a previously obtained rate token.
```
POST /api/v3/vendorpayment/fx-conversion
```

#### [FX Conversion Details](./FX_Conversion_Details.md)
Retrieve details of a specific FX conversion using its reference.
```
GET /api/v3/vendorpayment/fx-conversion/{reference}
```

#### [FX Conversion Webhooks](./FX_Conversion_02_Webhook.md)
Receive real-time updates on FX conversion status changes.

### Transfer Operations

#### [FX Transfer](./FX_Transfer_01.md)
Initiate cross-currency vendor payments using a previously obtained rate token.
```
POST /api/v3/vendorpayment/fx-transfer
```

#### [FX Transfer Details](./Get_FX_Transfer_By_Reference.md)
Retrieve FX transfer details by reference number.
```
GET /api/v3/vendorpayment/fx-transfer/{reference}
```

#### [FX Transfer Webhooks](./FX_Transfer_Webhook.md)
Receive real-time updates on FX transfer status changes.

#### [Internal Transfer](./Internal_Transfer.md)
Execute internal transfers between merchants on the platform.
```
POST /api/v3/vendorpayment/transfers
```

## Transaction Flow

### Foreign Exchange Transaction Flow

1. **Retrieve Exchange Rate**: Use the [FX Rate](./FX_Rate.md) endpoint to get a `rateToken` for a specific currency pair
2. **Execute Conversion**: Use the [FX Conversion](./FX_Conversion_01.md) endpoint with the `rateToken` to convert funds
3. **Monitor Status**: Track conversion status via [webhooks](./FX_Conversion_02_Webhook.md) or by querying the [FX Conversion Details](./FX_Conversion_Details.md) endpoint

### International Transfer Flow

1. **Retrieve Exchange Rate**: Use the [FX Rate](./FX_Rate.md) endpoint to get a `rateToken` for a specific currency pair
2. **Initiate Transfer**: Use the [FX Transfer](./FX_Transfer_01.md) endpoint with the `rateToken` and beneficiary details
3. **Monitor Status**: Track transfer status via [webhooks](./FX_Transfer_Webhook.md) or by querying the [FX Transfer Details](./Get_FX_Transfer_By_Reference.md) endpoint

## Webhooks

BudPay provides webhook notifications for real-time updates on transactions:

- **[FX Conversion Webhooks](./FX_Conversion_02_Webhook.md)**: Notify when currency conversions are processed
- **[FX Transfer Webhooks](./FX_Transfer_Webhook.md)**: Notify when international transfers change status

### Webhook Handling Best Practices

1. Validate webhook authenticity using HMAC signatures
2. Respond with HTTP status code 200 within 5 seconds
3. Implement idempotency using reference numbers
4. Log all webhook payloads for audit and debugging

## Error Handling

All endpoints return standardized error responses:

```json
{
  "success": false,
  "message": "Error message describing the issue",
  "code": "ERROR_CODE"
}
```

## Testing

Use the testing environment (identified by `domain: test` in responses) to validate your integration without affecting live data.

## Notes and Limitations

- Currency codes should use ISO 4217 format (e.g., USD, EUR, NGN)
- Country codes should use ISO 3166-1 alpha-2 format (e.g., GB, US)
- Rate tokens expire after a specified duration (typically 5 minutes)
- Transaction references must be unique for each operation
- For international transfers, ensure all bank details are accurate, including SWIFT/BIC codes