# BudPay Virtual Account API Overview

## Introduction
The BudPay Virtual Account API provides endpoints to create, retrieve, and manage virtual accounts. This documentation covers the following key functionalities:

1. [Get Virtual Account Details](#get-virtual-account-details)
2. [Retrieve Available Banks](#retrieve-available-banks)
3. [Create Virtual Account](#create-virtual-account)

---

## Get Virtual Account Details

### Overview
This endpoint allows you to retrieve details of a specific virtual account using the account number.

### Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-accounts/{accountNumber}`
- **Method**: GET
- **Authentication**: Bearer token required

### Response Fields
- `accountNumber`: The virtual account number
- `accountName`: The name associated with the account
- `bankCode`: The bank's code
- `bankName`: The bank's name
- `accountType`: Type of the virtual account (`reserved`, etc.)
- `accountStatus`: Status of the account (`active`, etc.)
- `expiryInMinutes`: Expiration time in minutes (0 means no expiration)

### Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/2041431102' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

---

## Retrieve Available Banks

### Overview
This endpoint fetches the list of banks available for virtual account creation.

### Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list`
- **Method**: GET
- **Authentication**: Bearer token required

### Response Fields
- `bankCode`: Unique identifier for each bank
- `bankName`: Name of the bank

### Sample Request
```bash
curl -X GET 'https://partners.budpay.com/api/v3/collection/virtual-accounts/bank-list' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

---

## Create Virtual Account

### Overview
This endpoint creates a new virtual account for a customer.

### Endpoint Details
- **URL**: `https://partners.budpay.com/api/v3/collection/virtual-account`
- **Method**: POST
- **Authentication**: Bearer token required

### Request Fields
- `reference`: Unique reference ID for the account
- `amount`: Expected amount (0 for unlimited transactions)
- `accountType`: Type of account (`reserved`, `checkout`)
- `accountName`: Display name for the account
- `bankCode`: Bank code (obtained from the bank list endpoint)
- `firstName`: Customer's first name
- `lastName`: Customer's last name
- `customerEmail`: Customer's email address
- `expiryInMinutes`: Time before expiration (0 for no expiration)

### Sample Request
```bash
curl -X POST 'https://partners.budpay.com/api/v3/collection/virtual-account' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "reference": "unique_reference_123",
    "amount": 0,
    "accountType": "reserved",
    "accountName": "CUSTOMER_ACCOUNT_NAME",
    "bankCode": "000017",
    "firstName": "Customer",
    "lastName": "Name",
    "customerEmail": "customer@example.com",
    "expiryInMinutes": 0
  }'
```

---

## Authentication
All endpoints require authentication using a Bearer token (API key) in the Authorization header.

---

## Conclusion
The BudPay Virtual Account API allows seamless management of virtual accounts, including fetching bank lists, retrieving account details, and creating new accounts securely.

