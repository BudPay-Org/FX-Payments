# Payout Webhook Documentation

This documentation explains the structure and purpose of the payout webhook notifications sent by the system to your endpoint.

---

## **Webhook Overview**

The payout webhook sends real-time notifications about the status of payouts. These notifications are triggered when a payout is processed, completed, or encounters an error.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object containing the following fields:

### Top-Level Fields

- **`notify`**: `"payout"`
Indicates this is a payout-related notification.
- **`notifyType`**: `"successful"`
Specifies the type of notification (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains detailed information about the payout transaction.

---

### **`data` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `id` | Integer | Unique internal ID for the payout transaction. |
| `reference` | String | Unique reference identifier for the payout (e.g., `BUD_trf_4fe1v.....`). |
| `sessionid` | String | Session ID associated with the transaction. |
| `currency` | String | Currency code of the payout (e.g., `NGN`). |
| `amount` | String | Payout amount in the specified currency (e.g., `"500000"`). |
| `fee` | String | Transaction fee deducted (e.g., `"100"`). |
| `bank_code` | String | Code of the beneficiary's bank (e.g., `090405`). |
| `bank_name` | String | Name of the beneficiary's bank (e.g., `Rolez Microfinance Bank`). |
| `account_number` | String | Beneficiary's account number (e.g., `0000222293`). |
| `account_name` | String | Beneficiary's account name (e.g., `Samuel Bud`). |
| `narration` | String | Transaction description or note (e.g., `"my narration"`). |
| `domain` | String | Environment where the transaction occurred (e.g., `live` or `test`). |
| `status` | String | Current status of the payout (e.g., `success`, `failed`, `pending`). |
| `settled_by` | Nullable | Reserved for future use (typically `null`). |
| `subaccount` | Nullable | Subaccount associated with the transaction (if applicable). |
| `created_at` | String | Timestamp of transaction creation (ISO 8601 format). |
| `updated_at` | String | Timestamp of the latest status update (ISO 8601 format). |

---

## **Example Webhook Payload**

```json
{
    "notify": "payout",
    "notifyType": "successful",
    "data": {
        "id": 4552,
        "reference": "BUD_trf_4fe1v.....",
        "sessionid": "110021221004050251.....",
        "currency": "NGN",
        "amount": "500000",
        "fee": "100",
        "bank_code": "090405",
        "bank_name": "Rolez Microfinance Bank",
        "account_number": "0000222293",
        "account_name": "Samuel Bud",
        "narration": "my narration",
        "domain": "live",
        "status": "success",
        "settled_by": null,
        "subaccount": null,
        "created_at": "2022-10-04T05:03:00.0000000000Z",
        "updated_at": "2022-10-04T05:03:03.000000Z"
    }
}
```

---

## **Handling Webhooks**

1. **Endpoint Security**:
    - Verify the authenticity of incoming webhooks by validating signatures (if provided by the API).
    - Use HTTPS to encrypt data in transit.
2. **Response Requirements**:
    - Return a `200 OK` HTTP status code to acknowledge receipt of the webhook.
    - Non-2xx responses may trigger retries by the sender.
3. **Idempotency**:
    - Use the `reference` or `id` field to detect duplicate notifications and prevent duplicate processing.

---

## **Key Fields for Reconciliation**

- **`reference`**: Use this unique ID to map transactions in your system.
- **`status`**: Check for `success`, `failed`, or `pending` to update internal records.
- **`amount` + `fee`**: Calculate net settlement amounts (e.g., `amount - fee` for deductions).

---

## **Error Scenarios**

- **`notifyType: "failed"`**:
Indicates a failed payout. Check the `status` and `data` fields for details.
- **Missing Fields**:
Log and investigate webhooks with incomplete data.

---

## **Testing Webhooks**

Use the `domain: "test"` flag in sandbox environments to simulate payloads without affecting live transactions.

---
