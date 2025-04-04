# Vendor Payment FX Conversion Webhook Documentation

This documentation explains the structure and purpose of the FX conversion webhook notifications for vendor payments. These notifications provide real-time updates on foreign exchange (FX) conversion transactions.

---

## **Webhook Overview**

The FX conversion webhook sends notifications about the status of FX conversions initiated through the vendor payment system. The payload includes details such as conversion rates, amounts, currencies, and transaction status.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object containing the following fields:

### Top-Level Fields

- **`notify`**: `"conversion"`
Indicates this is an FX conversion-related notification.
- **`notifyType`**: `"successful"`
Specifies the outcome of the transaction (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains detailed information about the FX conversion transaction.

---

### **`data` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `status` | String | Current status of the conversion (e.g., `pending`, `successful`). |
| `statusMessage` | String | Detailed message about the conversion status (e.g., `"Trade confirmed and processing"`). |
| `id` | Integer | Unique internal ID for the conversion transaction. |
| `rateToken` | String | Token representing the exchange rate used for the conversion. |
| `reference` | String | Unique reference identifier for the transaction. |
| `rate` | Float | Exchange rate applied for the conversion (e.g., `0.0006675567`). |
| `fromCurrency` | String | Currency code being converted from (e.g., `NGN`). |
| `toCurrency` | String | Currency code being converted to (e.g., `USD`). |
| `fromAmount` | Float | Amount in the source currency (e.g., `3000.00`). |
| `toAmount` | Float | Amount in the target currency after conversion (e.g., `2.00`). |

---

## **Example Webhook Payload**

```json
{
    "notify": "conversion",
    "notifyType": "successful",
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

---

## **Handling Webhooks**

### **1. Endpoint Security**

- **Signature Validation**: Verify the authenticity of incoming webhooks using HMAC signatures or other authentication mechanisms provided by BudPay.
- **HTTPS**: Ensure your webhook endpoint uses HTTPS to encrypt data in transit.


### **2. Response Requirements**

- **Acknowledgment**: Respond with an HTTP status code of **200 OK** within **5 seconds** to confirm receipt.
- **Logging**: Log all incoming webhooks for audit trails and debugging.


### **3. Idempotency**

- **Duplicate Handling**: Use the `reference` field to detect and prevent duplicate processing of the same transaction.


### **4. Reconciliation**

- **Transaction Matching**: Use the `reference` and `id` fields to reconcile transactions in your system.
- **Amount Verification**: Confirm that `fromAmount`, `toAmount`, and `rate` match your records.

---

## **Key Fields for Processing**

- **`status`**: Determines whether the conversion is pending, successful, or failed.
- **`rateToken`**: Validate that the rate token matches the one used during the initial conversion request.
- **`toAmount`**: Verify the converted amount against expected values.

---

## **Error Scenarios**

- **Failed Conversions**: If `notifyType` is `failed`, check `statusMessage` for details (e.g., rate expiration, insufficient funds).
- **Mismatched Data**: Log discrepancies between `fromAmount`, `toAmount`, and `rate` for manual review.

---

## **Testing Webhooks**

- **Sandbox Environment**: Use test environments (`domain: test` in other payloads) to simulate webhooks without affecting live transactions.
- **Payload Simulation**: Test edge cases (e.g., failed conversions, rate changes) to ensure proper handling.

---

## **Best Practices**

1. **Secure Storage**: Protect API keys and credentials using environment variables or vaults.
2. **Monitoring**: Set up alerts for unexpected statuses (e.g., `failed`) or missing fields.
3. **Documentation**: Keep a record of all webhook payload structures and field descriptions for reference.

---