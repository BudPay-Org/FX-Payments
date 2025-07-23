# Refund Webhook Documentation

This documentation explains the structure and handling of refund webhook notifications. These notifications provide real-time updates on refund transactions initiated through your payment system.

---

## **Webhook Overview**

The refund webhook sends notifications about the status of refunds, including key details such as the refund amount, currency, and processing status. Use this webhook to track refunds and update your records accordingly.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object containing the following fields:

### Top-Level Fields

- **`notify`**: `"refund"`
Indicates this is a refund-related notification.
- **`notifyType`**: `"successful"`
Specifies the outcome of the refund (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains detailed information about the refund transaction.

---

### **`data` Object Fields**

| Field | Type | Description | Nullable |
| :-- | :-- | :-- | :-- |
| `id` | Integer | Unique internal ID for the refund transaction. | No |
| `reference` | String | Original transaction reference (e.g., `Zotapay_6775575344`) | No |
| `refundReference` | String | Unique reference identifier for the refund (e.g., `BR1904MY6VHZOSSSP338`). | No |
| `amount` | String | Refund amount in the specified currency (e.g., `"500.00"`). | No |
| `currency` | String | Currency code of the refund (e.g., `GHS`). | No |
| `domain` | String | Environment where the transaction occurred (`live` or `test`). | No |
| `initiatedBy` | String | Who initiated the refund (`self`, `customer`, etc.). | No |
| `channel` | String | Channel used to initiate the refund (e.g., `API`, `Dashboard`). | No |
| `merchantNote` | String | Internal note provided by the merchant (e.g., reason for refund). | Yes |
| `customerNote` | String | Note visible to the customer (e.g., refund confirmation message). | Yes |
| `status` | String | Current status of the refund (e.g., `new`, `pending`, `success`, `awaiting approval`, `failed`). | No |
| `createdAt` | String | Timestamp of when the refund was initiated (ISO 8601 format). | No |

---

## **Example Webhook Payload**

```json
{
    "notify": "refund",
    "notifyType": "successful",
    "data": {
        "id": 41169,
        "reference": "Zotapay_6775575344",
        "refundReference": "BR1904MY6VHZOSSSP338",
        "amount": "500.00",
        "currency": "GHS",
        "domain": "test",
        "initiatedBy": "self",
        "channel": "API",
        "merchantNote": " refund for transaction Zotapay_6775575344",
        "customerNote": " refund for transaction Zotapay_6775575344",
        "status": "pending",
        "createdAt": "2025-04-04T02:20:48.0000000"
    }
}
```

---

## **Handling Webhooks**

### **1. Endpoint Security**

- **Signature Validation**: Verify incoming webhooks using HMAC signatures (if provided by your payment gateway).
- **HTTPS**: Ensure your endpoint uses HTTPS to encrypt data.


### **2. Response Requirements**

- **Acknowledgment**: Respond with `HTTP 200 OK` within **5 seconds** to confirm receipt.
- **Logging**: Log all webhook payloads for auditing and debugging.


### **3. Idempotency**

- **Duplicate Detection**: Use the `refundReference` field to prevent processing the same refund multiple times.


### **4. Reconciliation**

- **Transaction Matching**: Map refunds to original transactions using the `merchantNote` or `refundReference`.
- **Amount Verification**: Confirm the `amount` matches the expected refund value.

---

## **Key Fields for Processing**

- **`status`**: Determines whether the refund is pending, successful, or failed.
- **`initiatedBy`**: Identifies who requested the refund (e.g., merchant or customer).
- **`refundReference`**: Use this unique ID to track refunds in your system.

---

## **Error Scenarios**

- **Failed Refunds**: If `notifyType: "failed"`, check `status` and `merchantNote` for details.
- **Mismatched Data**: Log refunds with discrepancies between `amount` and original transaction values.

---

## **Testing Webhooks**

- **Sandbox**: Use `domain: "test"` to simulate refund webhooks without affecting live transactions.
- **Edge Cases**: Test scenarios like partial refunds, currency mismatches, and failed refunds.

---

## **Best Practices**

1. **Secure API Keys**: Store secret keys in environment variables or secure vaults.
2. **Monitor Statuses**: Set up alerts for `failed` refunds to resolve issues promptly.
3. **Customer Communication**: Use `customerNote` to provide clear refund updates to end-users.

---