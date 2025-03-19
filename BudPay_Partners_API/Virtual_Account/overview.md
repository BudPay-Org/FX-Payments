# BudPay Virtual Account API Overview

## Introduction
The BudPay Virtual Account API allows you to create, retrieve, and manage virtual accounts efficiently.

- [Get Virtual Account Details](#get-virtual-account-details) ([Docs](./Account_Number.md))
- [Retrieve Available Banks](#retrieve-available-banks) ([Docs](./Bank_List.md))
- [Create Virtual Account](#create-virtual-account) ([Docs](./Create_Virtual_Account.md))

---

## Get Virtual Account Details ([Docs](./Account_Number.md))
Retrieve details of a virtual account using its account number.

**Endpoint:** `GET /collection/virtual-accounts/{accountNumber}`

**Response Fields:**
- `accountNumber`, `accountName`, `bankCode`, `bankName`
- `accountType`, `accountStatus`, `expiryInMinutes`

**Sample Request:**
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/2041431102' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

---

## Retrieve Available Banks ([Docs](./Bank_List.md))
Fetch a list of banks available for virtual account creation.

**Endpoint:** `GET /collection/virtual-accounts/bank-list`

**Response Fields:**
- `bankCode`: Unique identifier
- `bankName`: Bank name

**Sample Request:**
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

---

## Create Virtual Account ([Docs](./Create_Virtual_Account.md))
Create a new virtual account for a customer.

**Endpoint:** `POST /collection/virtual-account`

**Required Fields:**
- `reference`, `amount`, `accountType`, `accountName`
- `bankCode`, `firstName`, `lastName`, `customerEmail`, `expiryInMinutes`

**Sample Request:**
```bash
curl -X POST 'https://partners.budpay.com/api/v3/collection/virtual-account' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{ "reference": "unique_ref", "amount": 0, "accountType": "reserved", "accountName": "Customer", "bankCode": "000017", "expiryInMinutes": 0 }'
```

---

## Authentication
All endpoints require a Bearer token (API key) in the Authorization header.

---

## Conclusion
The BudPay Virtual Account API simplifies virtual account creation and management, providing a seamless and secure experience.

