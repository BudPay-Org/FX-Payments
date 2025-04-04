# Virtual Account Webhook Documentation

This documentation explains the structure and purpose of the virtual account webhook notifications sent to your endpoint.

---

## **Webhook Overview**

The virtual account webhook sends real-time notifications when a transaction occurs on a dedicated virtual account. These notifications include details about deposits, fees, and customer information.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object containing the following fields:

### Top-Level Fields

- **`notify`**: `"transaction"`
Indicates this is a transaction-related notification.
- **`notifyType`**: `"successful"`
Specifies the outcome of the transaction (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains core transaction details.
- **`transferDetails`**:
Provides additional transfer-specific information.

---

### **`data` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `id` | Integer | Unique internal ID for the transaction. |
| `fees` | String | Transaction fee deducted (e.g., `"30"`). |
| `plan` | Nullable | Subscription plan associated with the transaction (if applicable). |
| `type` | String | Transaction type (e.g., `dedicated_account`). |
| `amount` | String | Actual amount received (e.g., `"20"`). |
| `domain` | String | Environment where the transaction occurred (`live` or `test`). |
| `status` | String | Transaction status (e.g., `success`). |
| `channel` | String | Payment channel used (e.g., `dedicated_account`). |
| `gateway` | String | Payment gateway processor (e.g., `wema`). |
| `message` | String | Human-readable transaction summary (e.g., `"Account credited successfully"`). |
| `paid_at` | String | Timestamp of payment completion (format: `dd/MM/yyyy HH:mm:ss`). |
| `currency` | String | Currency code of the transaction (e.g., `NGN`). |
| `customer` | Object | Contains beneficiary customer details (see below). |
| `reference` | String | Unique transaction reference (e.g., `100033250101140325860393638601`). |
| `created_at` | String | Transaction creation timestamp (ISO 8601 format). |
| `ip_address` | Nullable | IP address of the payer (if available). |
| `business_id` | Integer | ID of the business account associated with the transaction. |
| `customer_id` | Integer | ID of the customer making the payment. |
| `card_attempt` | Integer | Number of card payment attempts (if applicable). |
| `requested_amount` | String | Original requested amount (e.g., `"50.00"`). |

---

### **`customer` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `id` | Integer | Unique customer ID. |
| `email` | String | Customer's email address. |
| `phone` | String | Customer's phone number. |
| `domain` | String | Environment associated with the customer (`live` or `test`). |
| `status` | String | Customer account status (e.g., `active`). |
| `metadata` | String | Additional customer data in JSON format. |
| `last_name` | String | Customer's last name. |
| `first_name` | String | Customer's first name. |
| `customer_code` | String | Unique customer identifier (e.g., `CUS_ff0ondr3rxekzsd`). |

---

### **`transferDetails` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `amount` | String | Total transferred amount (e.g., `"50.00"`). |
| `bankcode` | String | Bank code of the virtual account provider (e.g., `100033`). |
| `bankname` | String | Name of the virtual account bank (e.g., `PALMPAY`). |
| `craccount` | String | Credit account number receiving funds. |
| `narration` | String | Transaction description (e.g., `"OLUWAKAYODE AYORINDE ADETUNJI:8031975397"`). |
| `sessionid` | String | Unique session ID matching the transaction reference. |
| `craccountname` | String | Name associated with the credit account. |
| `originatorname` | String | Name of the payer. |
| `paymentReference` | String | Unique payment reference matching `data.reference`. |
| `originatoraccountnumber` | String | Payer's account number. |

---

## **Example Webhook Payload**

```json
{
  "data": {
    "id": 14457138,
    "fees": "30",
    "plan": null,
    "type": "dedicated_account",
    "amount": "20",
    "domain": "live",
    "status": "success",
    "channel": "dedicated_account",
    "gateway": "wema",
    "message": "Account credited successfully",
    "paid_at": "01/01/2025 15:03:44",
    "currency": "NGN",
    "customer": {
      "id": 7608196,
      "email": "2532-adetunjioluwakayode@gmail.com",
      "phone": "08031975397",
      "domain": "live",
      "status": "active",
      "metadata": "{}",
      "last_name": "Adetunji",
      "first_name": "Kayode",
      "customer_code": "CUS_ff0ondr3rxekzsd"
    },
    "reference": "100033250101140325860393638601",
    "created_at": "2025-01-01T15:03:44",
    "ip_address": null,
    "business_id": 30,
    "customer_id": 7608196,
    "card_attempt": 0,
    "requested_amount": "50.00"
  },
  "notify": "transaction",
  "notifyType": "successful",
  "transferDetails": {
    "amount": "50.00",
    "bankcode": "100033",
    "bankname": "PALMPAY",
    "craccount": "4051242100",
    "narration": "OLUWAKAYODE AYORINDE ADETUNJI:8031975397",
    "sessionid": "100033250101140325860393638601",
    "craccountname": "Inclusive 1 / Kayode Adetunji",
    "originatorname": "OLUWAKAYODE AYORINDE ADETUNJI",
    "paymentReference": "100033250101140325860393638601",
    "originatoraccountnumber": "8031975397"
  }
}
```

---

## **Handling Webhooks**

1. **Endpoint Security**:
    - Verify payload authenticity using HMAC signatures (if provided).
    - Restrict access to trusted IP addresses.
2. **Response Requirements**:
    - Respond with `HTTP 200 OK` within **5 seconds** to acknowledge receipt.
    - Log all webhooks for audit trails.
3. **Reconciliation**:
    - Use `data.reference` and `transferDetails.paymentReference` to match transactions.
    - Compare `data.requested_amount` and `transferDetails.amount` for amount validation.

---

## **Key Fields for Processing**

- **`data.status`**: Determines success/failure of the transaction.
- **`data.customer.customer_code`**: Links the transaction to your internal customer records.
- **`transferDetails.craccount`**: Identifies the virtual account credited.

---

## **Error Scenarios**

- **`notifyType: "failed"`**: Indicates a failed transaction. Check `data.message` for details.
- **Mismatched amounts**: Investigate if `data.amount` differs significantly from `transferDetails.amount`.

---

## **Testing**

Use `domain: "test"` in sandbox environments to simulate transactions without live financial impact.

---

This concludes the Virtual Account Webhook documentation.

---

# Virtual Account Webhook Documentation

This documentation provides details on the structure and handling of virtual account webhook notifications. These notifications are triggered when a transaction occurs on a dedicated virtual account.

---

## **Webhook Overview**

The virtual account webhook sends real-time notifications about transactions such as deposits or credits to a dedicated virtual account. The payload contains transaction details, customer information, and transfer specifics.

---

## **Webhook Payload Structure**

The webhook payload is a JSON object with the following structure:

### Top-Level Fields

- **`notify`**: `"transaction"`
Identifies the type of notification (in this case, a transaction-related event).
- **`notifyType`**: `"successful"`
Indicates the status of the notification (e.g., `successful`, `failed`, `pending`).
- **`data`**:
Contains core transaction details.
- **`transferDetails`**:
Provides additional details about the transfer.

---

### **`data` Object Fields**

| Field | Type | Description |
| :-- | :-- | :-- |
| `id` | Integer | Unique internal ID for the transaction. |
| `fees` | String | Transaction fee deducted (e.g., `"30"`). |
| `plan` | Nullable | Subscription plan associated with the transaction (if applicable). |
| `type` | String | Transaction type (e.g., `dedicated_account`). |
| `amount` | String | Actual amount received in the transaction (e.g., `"20"`). |
| `domain` | String | Environment where the transaction occurred (`live` or `test`). |
| `status` | String | Transaction status (e.g., `success`). |
| `channel` | String | Payment channel used (e.g., `dedicated_account`). |
| `gateway` | String | Payment gateway processor (e.g., `wema`). |
| `message` | String | Human-readable message describing the transaction outcome. |
| `paid_at` | String | Timestamp of payment completion (format: `dd/MM/yyyy HH:mm:ss`). |
| `currency` | String | Currency code of the transaction (e.g., `NGN`). |
| `customer` | Object | Contains customer details (see below). |
| `reference` | String | Unique reference identifier for the transaction. |
| `created_at` | String | Timestamp of when the transaction was created (ISO 8601 format). |
| `ip_address` | Nullable | IP address of the payer (if available). |
| `business_id` | Integer | ID of the business associated with this transaction. |
| `customer_id` | Integer | ID of the customer making the payment. |
| `card_attempt` | Integer | Number of card payment attempts made for this transaction. |
| `requested_amount` | String | Original requested amount for the transaction (e.g., `"50.00"`). |

---

### **Customer Object Fields**

The customer object contains details about the individual or entity making the payment.


| Field | Type | Description |
| :-- | :-- | :-- |
| `id` | Integer | Unique ID of the customer. |
| `email` | String | Customer's email address. |
| `phone` | String | Customer's phone number. |
| `domain` | String | Environment associated with this customer (`live`, etc.). |
| `status` | String | Status of the customer's account (`active`, etc.). |
| `metadata` | String | Additional metadata related to the customer in JSON format. |
| `last_name` | String | Customer's last name. |
| `first_name` | String | Customer's first name. |
| `customer_code` | String | Unique code identifying this customer in your system. |

---

### **TransferDetails Object Fields**

The transferDetails object provides additional information about the transfer process.


| Field | Type | Description |
| :-- | :-- | :-- |
| `amount` | String | Total transferred amount (e.g., `"50.00"`). |
| `bankcode` | String | Bank code associated with the virtual account provider. |
| `bankname` | String | Name of the bank handling the virtual account (e.g., `"PALMPAY"`). |
| `craccount` | String | Credit account number receiving funds. |
| `narration` | String | Description or note for this transaction (e.g., payer's name and phone). |
| `sessionid` | String | Unique session ID matching this transaction reference. |
| `craccountname` | String | Name associated with the credit account receiving funds. |
| `originatorname` | String | Name of the payer initiating this transfer. |
| `paymentReference` | String | Unique reference identifier for this payment, matching data.reference. |
| `originatoraccountnumber` | String | Account number of the payer initiating this transfer. |

---

## **Example Webhook Payload**

```json
{
  "data": {
    "id": 14457138,
    "fees": "30",
    "plan": null,
    "type": "dedicated_account",
    "amount": "20",
    "domain": "live",
    "status": "success",
    "channel": "dedicated_account",
    "gateway": "wema",
    "message": "Account credited successfully",
    "paid_at": "01/01/2025 15:03:44",
    "currency": "NGN",
    "customer": {
      "id": 7608196,
      "email": "2532-adetunjioluwakayode@gmail.com",
      "phone": "08031975397",
      "domain": "live",
      "status": "active",
      "metadata": "{}",
      "last_name": "Adetunji",
      "first_name": "Kayode",
      "customer_code": "CUS_ff0ondr3rxekzsd"
    },
    "reference": "100033250101140325860393638601",
    "created_at": "2025-01-01T15:03:44",
    "ip_address": null,
    "business_id": 30,
    "customer_id": 7608196,
    "card_attempt": 0,
    "requested_amount": "50.00"
  },
  "notify": "transaction",
  "notifyType": "successful",
  "transferDetails": {
    "amount": "50.00",
    "bankcode": "100033",
    "bankname": "PALMPAY",
    "craccount": "4051242100",
    "narration": "OLUWAKAYODE AYORINDE ADETUNJI:8031975397",
    "sessionid": "100033250101140325860393638601",
    "craccountname": "Inclusive 1 / Kayode Adetunji",
    "originatorname": "OLUWAKAYODE AYORINDE ADETUNJI",
    "paymentReference": "100033250101140325860393638601",
    "originatoraccountnumber": "8031975397"
  }
}
```

---

## **Handling Webhooks**

1. **Endpoint Security**:
    - Validate incoming webhooks using HMAC signatures or other verification methods.
    - Ensure your endpoint uses HTTPS to secure data in transit.
2. **Response Requirements**:
    - Respond with an HTTP status code of **200 OK** within a few seconds to acknowledge receipt.
    - Log all webhook payloads for debugging and reconciliation purposes.
3. **Idempotency**:
    - Use unique fields like `"reference"` or `"sessionid"` to ensure that duplicate notifications are not processed multiple times.
4. **Reconciliation**:
    - Match transactions using fields like `"reference"`, `"paymentReference"`, or `"sessionid"`.
    - Verify amounts (`data.amount`, `transferDetails.amount`) to ensure consistency.

---

## **Error Scenarios**

- If `"notifyType"` is set to `"failed"`, investigate using fields like `"message"` and `"status"`.
- Missing or incomplete fields should be logged and flagged for manual review.

---

## **Testing Webhooks**

Use test environments (`domain: test`) to simulate webhook payloads without affecting live data.

---