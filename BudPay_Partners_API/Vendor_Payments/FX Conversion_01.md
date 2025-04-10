# FX Conversion API Documentation

The FX Conversion endpoint allows you to execute a currency conversion transaction using a previously obtained rate token. This endpoint finalizes the conversion process at the locked-in exchange rate.

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


| Parameter | Description | Required | Type |
|-----------|-------------|----------|------|
| `rateToken` | The unique token obtained from a previous [FX Rate](./FX_Rate.md) FX rate request that locks in the exchange rate | Yes | string |
| `reference` | A unique reference identifier for this conversion transaction | Yes | string |


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

In case of errors, the API will return an appropriate error message and status code.


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
    "message": "Invalid rate token"
}
```

```json
{
    "status": false,
    "message": "Expired rate token"
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
| 400 | Invalid rate token | The provided rate token is not valid |
| 400 | Expired rate token | The rate token has expired |
| 500 | An internal error occurred please try again | Server encountered an error |


## Usage Notes

1. This endpoint should be called after obtaining a valid `rateToken` from the FX Rate endpoint.
2. The `reference` parameter should be unique for each transaction to ensure proper tracking.
3. The exchange rate used for the conversion is the one associated with the provided `rateToken`.
4. Ensure the `rateToken` hasn't expired before making this request (check the `rateExpiry` from the FX Rate response).
5. The response will contain the status of the conversion, which may be immediate or pending depending on the system configuration.