# Vendor Payment FX Transfer Webhook Documentation

This documentation explains the structure and handling of the FX transfer webhook notifications for vendor payments. These notifications provide real-time updates on foreign exchange (FX) transfer transactions.

---

## **Webhook Overview**

The FX transfer webhook sends notifications about the status of FX transfers initiated through the vendor payment system. The payload includes details about the transaction, such as currencies involved, amounts, and beneficiary bank information.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object containing the following fields:

### Top-Level Fields

- **`notify`**: `"fx-transfer"`
Indicates this is an FX transfer-related notification.
- **`notifyType`**: `"successful"`
Specifies the type of notification (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains detailed information about the FX transfer transaction.

---

### **`data` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `status` | String | Current status of the FX transfer (e.g., `pending`, `successful`). |
| `fromCurrency` | String | Currency code being sold (e.g., `NGN`). |
| `toCurrency` | String | Currency code being bought (e.g., `USD`). |
| `buyAmount` | Float | Amount in the target currency being purchased (e.g., `2.00`). |
| `sellAmount` | Float | Amount in the source currency being sold (e.g., `3000.00`). |
| `bankCountry` | String | Country code of the beneficiary bank (e.g., `GB`). |
| `bankName` | String | Name of the beneficiary bank (e.g., `Citibank NA`). |
| `accountNumber` | String | Beneficiary's account number or IBAN (e.g., `GB50CITI185008133062560`). |
| `accountName` | String | Name associated with the beneficiary account (e.g., `BudPay`). |
| `swiftCode` | String | SWIFT/BIC code of the beneficiary bank (e.g., `CITIGB2LXXX`). |
| `narration` | String | Description or note for the transaction (e.g., `"Test"`). |
| `reference` | String | Unique reference identifier for the transaction. |
| `domain` | String | Environment where the transaction occurred (`live`, `test`, etc.). |
| `createdAt` | String | Timestamp of when the transaction was created (ISO 8601 format). |
| `updatedAt` | String | Timestamp of the most recent status update for this transaction. |

---

## **Example Webhook Payload**

```json
{
    "notify": "fx-transfer",
    "notifyType": "successful",
    "data": {
        "status": "pending",
        "fromCurrency": "NGN",
        "toCurrency": "USD",
        "buyAmount": 2.00,
        "sellAmount": 3000.00,
        "bankCountry": "GB",
        "bankName": "Citibank NA",
        "accountNumber": "GB50CITI185008133062560",
        "accountName": "BudPay",
        "swiftCode": "CITIGB2LXXX",
        "narration": "Test",
        "reference": "202504041256005",
        "domain": "test",
        "createdAt": "2025-04-04T00:49:22",
        "updatedAt": "2025-04-04T00:49:37"
    }
}
```

---

## **Handling Webhooks**

### **1. Endpoint Security**

- Validate incoming webhooks using HMAC signatures or other authentication mechanisms provided by BudPay.
- Ensure your endpoint uses HTTPS to encrypt data in transit.


### **2. Response Requirements**

- Respond with an HTTP status code of **200 OK** within a few seconds to acknowledge receipt.
- Log all webhook payloads for debugging and reconciliation purposes.


### **3. Idempotency**

- Use unique fields like `"reference"` to ensure duplicate notifications are not processed multiple times.


### **4. Reconciliation**

- Match transactions using fields like `"reference"`.
- Verify amounts (`buyAmount`, `sellAmount`) and currency codes (`fromCurrency`, `toCurrency`) to ensure consistency.

---

## **Key Fields for Processing**

1. **Transaction Status**:
    - Use `"status"` to determine whether the transaction is pending, successful, or failed.
2. **Reference**:
    - Use `"reference"` as a unique identifier to track and reconcile transactions in your system.
3. **Beneficiary Details**:
    - Verify `"bankName"`, `"accountNumber"`, and `"swiftCode"` against your records before processing further.
4. **Amounts**:
    - Confirm `"buyAmount"` and `"sellAmount"` align with expected values for the transaction.

---

## **Error Scenarios**

### Failed Transactions

If `"notifyType"` is set to `"failed"`, investigate using fields like `"status"`, `"narration"`, and timestamps (`createdAt`, `updatedAt`) for troubleshooting.

### Missing or Invalid Data

Log and flag webhook payloads with missing or invalid fields for manual review.

---

## **Testing Webhooks**

Use test environments (`domain: test`) to simulate webhook payloads without affecting live data.

---

## **Best Practices**

1. Secure storage of API keys and credentials.
2. Implement rate limiting on your webhook endpoint to prevent abuse.
3. Log all incoming webhooks for audit trails and debugging purposes.
4. Regularly monitor webhook activity for anomalies or suspicious behavior.

---