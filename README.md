# BudPay FX API Documentation

## Overview

The BudPay FX API provides a comprehensive solution for currency conversion operations. This API allows partners to obtain real-time exchange rates, execute currency conversions, and check the status of conversion transactions. The API is designed to be straightforward and secure, requiring API key authentication for all endpoints.

## Authentication

All API endpoints require authentication using a Bearer token:

```
Authorization: Bearer YOUR_API_KEY
```

Replace `YOUR_API_KEY` with your actual API key provided by BudPay.

## API Workflow

The typical workflow for using the BudPay FX API consists of three main steps:

1. **Get Exchange Rate**: Obtain current exchange rates and a rate token
2. **Execute Conversion**: Perform the currency conversion using the rate token
3. **Check Conversion Status**: Verify the status of the conversion transaction

## Available Endpoints

### 1. FX Rate Endpoint

**Endpoint**: `POST https://partners.budpay.com/api/v3/vendorpayment/fx-rate`

This endpoint provides exchange rates between two currencies and allows you to calculate equivalent amounts in either currency. The response includes a `rateToken` that locks in the exchange rate for a limited time.

**Key Features**:
- Get real-time exchange rates
- Convert amounts from one currency to another
- Obtain a rate token for executing conversions

### 2. FX Conversion Endpoint

**Endpoint**: `POST https://partners.budpay.com/api/v3/vendorpayment/fx-conversion`

This endpoint executes a currency conversion transaction using a previously obtained rate token. The conversion is performed at the locked-in exchange rate.

**Key Features**:
- Execute currency conversions
- Use locked-in exchange rates
- Track conversions with unique reference IDs

### 3. Get FX Conversion Status Endpoint

**Endpoint**: `GET https://partners.budpay.com/api/v3/vendorpayment/fx-conversion/{reference}`

This endpoint allows you to check the status and details of a previously initiated conversion transaction using its unique reference identifier.

**Key Features**:
- Track conversion status
- Retrieve conversion details
- Verify transaction completion

## Important Notes

1. Rate tokens have a limited validity period. Check the `rateExpiry` and `rateValidityInSeconds` fields in the FX Rate response.
2. Always use unique reference identifiers for conversion transactions to ensure proper tracking.
3. The conversion status may not be immediate. Use the status endpoint to check for completion.
4. Ensure your API requests include all required parameters to avoid Bad Request errors.

## Additional Documentation

For detailed information about each endpoint, including request parameters, response formats, and error codes, please refer to the following documentation:

- [FX Rate Endpoint Documentation](./FX_Rate_README.md)
- [FX Conversion Endpoint Documentation](./FX_Conversion_README.md)
- [FX Conversion Status Endpoint Documentation](./FX_Conversion_Status_README.md)
