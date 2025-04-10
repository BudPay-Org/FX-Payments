# FX Conversion Details API Documentation

This documentation explains how to retrieve details of a specific foreign exchange (FX) conversion for vendor payments using the API endpoint.

---

## **Endpoint**

```
GET https://partners.budpay.com/api/v3/vendorpayment/fx-conversion/{reference}
```

Replace `{reference}` with the unique identifier for the FX conversion.

---

## **Headers**

- **Authorization**: `{{SecretKey}}`
Your API key or secret key for authentication.

---

## **cURL Example**

Below is an example of how to retrieve FX conversion details using `curl`:

```bash
curl -X GET 'https://partners.budpay.com/api/v3/vendorpayment/fx-conversion/202504041256007' \
--header 'Authorization: {{SecretKey}}'
```

---

## **Response**

The API returns a JSON response containing the details of the FX conversion. Below is an example of a successful response:

### Example Response:

```json
{
    "status": true,
    "message": "Fx Conversion details retrieved",
    "data": {
        "status": "pending",
        "statusMessage": "Trade confirmed and processing",
        "id": 2,
        "rateToken": "bfxtSPYEMNY3MQARGFO3",
        "reference": "202504041256007",
        "rate": 0.0006675567,
        "fromCurrency": "NGN",
        "toCurrency": "USD",
        "fromAmount": 3000.00,
        "toAmount": 2.00
    }
}
```


### Response Fields:

| Field | Type | Description | Nullable |
| :-- | :-- | :-- | :-- |
| `status` | Boolean | Indicates if the request was successful. | No |
| `message` | String | Describes the outcome of the request. | No |
| `data.status` | String | Current status of the FX conversion process. | No |
| `data.statusMessage` | String | Detailed message about the conversion status. | No |
| `data.id` | Integer | Unique identifier for the conversion transaction. | No |
| `data.rateToken` | String | Token used for this FX rate conversion. | No |
| `data.reference` | String | Reference number provided in the request. | No |
| `data.rate` | Float | Exchange rate applied for conversion. | No |
| `data.fromCurrency` | String | Currency being converted from (ISO code). | No |
| `data.toCurrency` | String | Currency being converted to (ISO code). | No |
| `data.fromAmount` | Float | Amount in source currency being converted. | No |
| `data.toAmount` | Float | Amount in target currency after conversion. | No |

---

## **Error Handling**

The API may return the following error responses:

### 401 Unauthorized
```json
{
    "status": false,
    "message": "Invalid Merchant Authorization"
}
```

### 404 Not Found
```json
{
    "status": false,
    "message": "No record found"
}
```

### 500 Internal Server Error
```json
{
    "status": false,
    "message": "An internal error occurred please try again"
}
```

### Error Details
| Status Code | Message | Description |
|------------|---------|-------------|
| 401 | Invalid Merchant Authorization | API key is missing, invalid or expired |
| 404 | No record found | Conversion with specified reference does not exist |
| 500 | An internal error occurred please try again | Server encountered an error processing the request |

---

## **Notes**

- Replace placeholders like `{{SecretKey}}`, and `{reference}` with actual values.
- Use secure methods to store and retrieve your API keys to prevent unauthorized access.
