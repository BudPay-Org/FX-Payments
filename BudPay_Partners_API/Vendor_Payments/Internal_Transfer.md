# Internal Transfer for Vendor Payment API Documentation

This documentation explains how to initiate an internal transfer for vendor payments using the API endpoint.

---

## **Endpoint**

```
POST https://partners.budpay.com/api/v3/vendorpayment/transfers
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
| `fromCurrency` | String | Currency code to transfer from (e.g., `NGN`). |
| `toCurrency` | String | Currency code to transfer to (e.g., `GHS`). |
| `transactionReference` | String | Unique reference for the transaction. |
| `beneficiaryMerchantId` | Integer | Unique identifier for the beneficiary merchant. |
| `beneficiaryMerchantName` | String | Name of the beneficiary merchant. |
| `amount` | Float | Amount to transfer in the source currency (e.g., `1000.00` in `NGN`). |

### Example Request Body:

```json
{
  "fromCurrency": "NGN",
  "toCurrency": "GHS",
  "transactionReference": "202504041256008",
  "beneficiaryMerchantId": 16686,
  "beneficiaryMerchantName": "Majorsignature94",
  "amount": 1000
}
```

---

## **cURL Example**

Below is an example of how to make a request using `curl`:

```bash
curl -X POST 'https://partners.budpay.com/api/v3/vendorpayment/transfers' \
--header 'Authorization: {{SecretKey}}' \
--header 'Content-Type: application/json' \
--data '{
  "fromCurrency": "NGN",
  "toCurrency": "GHS",
  "transactionReference": "202504041256008",
  "beneficiaryMerchantId": 16686,
  "beneficiaryMerchantName": "Majorsignature94",
  "amount": 1000
}'
```

---

## **Response**

The API returns a JSON response confirming the transaction status. Below is an example of a successful response:

### Example Response:

```json
{
    "success": true,
    "message": "Transaction completed successfully",
    "data": {
        "responseCode": "00",
        "responseDescription": "successful",
        "fromCurrency": "NGN",
        "toCurrency": "GHS",
        "transactionReference": "202504041256008",
        "beneficiaryMerchantId": 16686,
        "amount": 1000,
        "transactionRate": 0.0099901000,
        "finalCreditAmount": 9.99000,
        "friendlyRateDisplay": 0
    }
}
```


### Response Fields:

| Field | Type | Description |
| :-- | :-- | :-- |
| `success` | Boolean | Indicates if the request was successful. |
| `message` | String | Describes the outcome of the request. |
| `data.responseCode` | String | Code representing the transaction status (e.g., `00` for success). |
| `data.responseDescription` | String | Detailed description of the transaction status (e.g., `successful`). |
| `data.fromCurrency` | String | Source currency of the transfer. |
| `data.toCurrency` | String | Target currency of the transfer. |
| `data.transactionReference` | String | Unique reference used in the request. |
| `data.beneficiaryMerchantId` | Integer | ID of the beneficiary merchant. |
| `data.amount` | Float | Amount transferred in the source currency. |
| `data.transactionRate` | Float | Exchange rate applied for the conversion. |
| `data.finalCreditAmount` | Float | Amount credited to the beneficiary in the target currency. |
| `data.friendlyRateDisplay` | Integer | Human-readable representation of the rate (e.g., `0` for spot rates). |

---

## **Error Handling**

In case of errors, the API will return an appropriate error message and status code.

### Example Error Response:

```json
{
    "success": false,
    "message": "Invalid beneficiary merchant ID",
    "data": null
}
```

---

## **Notes**

- Replace placeholders like `{{SecretKey}}` with actual values.
- Ensure `beneficiaryMerchantId` corresponds to a valid merchant account.
- Use secure methods to store and retrieve your API keys to prevent unauthorized access.