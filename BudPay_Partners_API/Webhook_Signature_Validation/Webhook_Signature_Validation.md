# Webhook Signature Validation Documentation

This documentation explains how to validate webhook signatures to ensure the authenticity of incoming webhook requests. Validating webhook signatures is crucial for preventing unauthorized or fraudulent attempts to interact with your system.

---

## **Overview**

Webhook signature validation involves comparing a computed signature (using your secret key) with the signature provided in the webhook header. If the signatures match, the webhook request is authentic and can be processed. If they do not match, the request should be rejected.

---

## **Steps for Validation**

### **1. Compute Merchant Signature**

Use your **BudPay Secret Key** and **BudPay Public Key** to generate a merchant signature using the `SHA512` hashing algorithm.

#### Example Code:

```php
$sec = "YOUR_BUDPAY_SECRET_KEY"; // Replace with your BudPay Secret Key
$pub = "YOUR_BUDPAY_PUBLIC_KEY"; // Replace with your BudPay Public Key
$merchantsignature = hash_hmac("SHA512", $pub, $sec); // Generate merchant signature
```


### **2. Retrieve Webhook Signature**

The webhook signature is located in the **header** of the incoming webhook request. This signature is sent by BudPay to verify the authenticity of the webhook.

#### Example:

```php
$webhooksignature = "THE MERCHANT SIGNATURE LOCATED IN THE HEADER OF THE WEBHOOK RECEIVED"; // Replace with actual header value
```


### **3. Compare Signatures**

Compare the computed `merchantsignature` with the `webhooksignature` received in the header.

#### Example Code:

```php
if ($merchantsignature != $webhooksignature) {
    echo "DON’T HONOUR. IT IS A FRAUDULENT ATTEMPT";
} else {
    echo "THE TRANSACTION WAS INITIATED BY YOU AND THUS BELONGS TO YOU";
}
```

---

## **Detailed Explanation**

### **Hashing Algorithm**

- The `SHA512` hashing algorithm is used for generating a secure hash.
- The `hash_hmac` function combines your public key and secret key securely to compute a unique merchant signature.


### **Webhook Header**

- BudPay sends a signature in the webhook header for every request.
- This signature ensures that only authorized webhooks are processed.


### **Validation Logic**

- If the computed `merchantsignature` matches the `webhooksignature`, it confirms that BudPay initiated the transaction.
- If they do not match, reject the webhook as it may be fraudulent.

---

## **PHP Implementation Example**

Below is a complete PHP implementation for validating webhook signatures:

```php
    $sec = "YOUR_BUDPAY_SECRET_KEY";
    $pub = "YOUR_BUDPAY_PUBLIC KEY";
    $merchantsignature =  hash_hmac("SHA512", $pub,$sec);
    $webhooksignature = "THE MERCHANT SIGNATURE LOCATED IN THE HEADER OF THE WEBHOOK RECEIVED";

    if($merchantsignature != $webhooksignature) {
        "DON’T HONOUR. IT IS A FRAUDULENT ATTEMPT";
    }

    if($merchantsignature == $webhooksignature) {
        "THE TRANSACTION WAS INITIATED BY YOU AND THUS BELONGS TO YOU";
    }
```

---

## **Error Handling**

- **Missing Header**: If the webhook signature header is missing, reject the request immediately.
- **Signature Mismatch**: Log all mismatched signatures for auditing and investigation.
- **Invalid Keys**: Ensure that your secret and public keys are stored securely and are not exposed publicly.

---

## **Best Practices**

1. **Secure Storage**: Store your secret key securely (e.g., in environment variables or encrypted storage).
2. **HTTPS**: Ensure your endpoint uses HTTPS to encrypt data in transit.
3. **Logging**: Log all incoming webhook requests for debugging and reconciliation purposes.
4. **Rate Limiting**: Implement rate limiting on your endpoint to prevent abuse or brute-force attempts.

---

## **Testing Webhook Validation**

1. Simulate incoming webhooks in a test environment using valid and invalid signatures.
2. Verify that valid signatures are processed correctly while invalid ones are rejected.

---