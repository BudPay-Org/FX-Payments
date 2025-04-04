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

| Field | Type | Description |
| :-- | :-- | :-- |
| `status` | Boolean | Indicates if the request was successful. |
| `message` | String | Describes the outcome of the request. |
| `data.status` | String | Current status of the FX conversion process. |
| `data.statusMessage` | String | Detailed message about the conversion status. |
| `data.id` | Integer | Unique identifier for the conversion transaction. |
| `data.rateToken` | String | Token used for this FX rate conversion. |
| `data.reference` | String | Reference number provided in the request. |
| `data.rate` | Float | Exchange rate applied for conversion. |
| `data.fromCurrency` | String | Currency being converted from (ISO code). |
| `data.toCurrency` | String | Currency being converted to (ISO code). |
| `data.fromAmount` | Float | Amount in source currency being converted. |
| `data.toAmount` | Float | Amount in target currency after conversion. |

---

## **Error Handling**

In case of errors, the API will return an appropriate error message and status code.

### Example Error Response:

```json
{
    "status": false,
    "message": "Conversion details not found"
}
```

---

## **Notes**

- Replace placeholders like `{{SecretKey}}`, and `{reference}` with actual values.
- Use secure methods to store and retrieve your API keys to prevent unauthorized access.
