# FX Conversion API Documentation

This documentation provides details on how to initiate a foreign exchange (FX) conversion using the API endpoint.

---

## **Endpoint**

```
POST https://partners.budpay.com/api/v3/vendorpayment/fx-conversion
```

---

## **Headers**

- **Authorization**: `{{SecretKey}}`
Your API key or secret key for authentication.
- **Content-Type**: `application/json`
Specifies the format of the request body.

---

## **Request Body**

The request body should be in JSON format and include the following parameters:


| Parameter | Type | Description |
| :-- | :-- | :-- |
| `rateToken` | String | Token representing the exchange rate to use. |
| `reference` | String | Unique reference for the transaction. |

### Example:

```json
{
  "rateToken": "bfxtSPYEMNY3MQARGFO3",
  "reference": "202504041256007"
}
```

---

## **cURL Example**

Below is an example of how to make a request using `curl`:

```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/fx-conversion' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data '{
  "rateToken": "bfxtSPYEMNY3MQARGFO3",
  "reference": "202504041256007"
}'
```

---

## **Response**

The API returns a JSON response indicating the status of the FX conversion. Below is an example of a successful response:

### Example Response:

```json
{
    "status": true,
    "message": "Fx Conversion Initiated",
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
    "message": "Invalid rate token provided"
}
```

