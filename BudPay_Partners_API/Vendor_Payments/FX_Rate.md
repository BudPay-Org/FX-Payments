# Vendor Payment FX Rate API Documentation

## Overview
The FX Rate endpoint provides currency conversion rates between two specified currencies and can be used to calculate equivalent amounts in either the source or target currency.

## Endpoint
```
POST https://partners.budpay.com/api/v3/vendorpayment/fx-rate
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
| fromCurrency | String | Yes | The source currency code (e.g., "NGN") |
| toCurrency | String | Yes | The target currency code (e.g., "USD") |
| fromAmount | Number | Yes | The amount in the source currency |
| toAmount | Number | Yes | The amount in the target currency (typically set to 0 when requesting a conversion) |

## Example Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/fx-rate' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data '{
    "fromCurrency": "NGN",
    "toCurrency": "USD",
    "fromAmount": 3000,
    "toAmount": 0
}'
```

## Example Response
```json
{
    "status": true,
    "message": "Vendor rates retrieved",
    "data": {
        "rateToken": "bfxtSPYEMNY3MQARGFO3",
        "rate": 0.0006675567,
        "rateExpiry": "2025-04-04T02:21:26.9817662+01:00",
        "rateValidityInSeconds": 300,
        "fromCurrency": "NGN",
        "toCurrency": "USD",
        "fromAmount": 3000,
        "toAmount": 2.0026701000
    }
}
```

## Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| status | Boolean | Status of the request (true for success) |
| message | String | A description of the outcome |
| data.rateToken | String | Unique token for this exchange rate |
| data.rate | Number | The exchange rate applied |
| data.rateExpiry | String | ISO 8601 timestamp indicating when the rate expires |
| data.rateValidityInSeconds | Number | How long the rate is valid in seconds |
| data.fromCurrency | String | The source currency code |
| data.toCurrency | String | The target currency code |
| data.fromAmount | Number | The amount in the source currency |
| data.toAmount | Number | The calculated amount in the target currency |

## Error Responses
If the request fails, the API will return an error response:

```json
{
  "status": false,
  "message": "Error message describing the issue",
  "code": "ERROR_CODE"
}
```

## Notes
- Currency codes should be provided in the ISO 4217 format (e.g., USD, EUR, NGN).
- If toAmount is set to a value other than 0, the system will calculate the fromAmount based on the provided toAmount.
- Exchange rates are subject to change and are updated regularly.
- Rate tokens are valid for the duration specified in rateValidityInSeconds (typically 5 minutes).