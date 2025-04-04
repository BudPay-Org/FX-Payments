# Get Virtual Accounts Details Endpoint Documentation

## Get Virtual Account Details by Account Number

### Endpoint
`GET https://partners.budpay.com/api/v3/collection/virtual-accounts/{accountNumber}`

### Description
Retrieve details of a virtual account using its account number.

### Request Parameters
| Parameter      | Type   | Description                         |
|-------------- |--------|-------------------------------------|
| accountNumber | string | The virtual account number to fetch |

### Response
#### Success Response
```json
{
    "status": true,
    "message": "Virtual Account List Retrieved",
    "data": [
        {
            "accountNumber": "4050910184",
            "accountName": "Isaiah Falade",
            "bankCode": "000031",
            "bankName": "Premium Trust Bank",
            "accountType": "reserved",
            "accountStatus": "active",
            "expiryInMinutes": 0,
            "reference": "20250404000002",
            "createdAt": "2025-04-03T23:25:53"
        }
    ]
}
```

---

## Get Virtual Accounts Details by Reference

### Endpoint
`GET https://partners.budpay.com/api/v3/collection/virtual-account/{reference}`

### Description
Retrieve details of a virtual account using its reference.

### Request Parameters
| Parameter  | Type   | Description                        |
|-----------|--------|------------------------------------|
| reference | string | The unique reference of the account |

### Response
#### Success Response
```json
{
    "status": true,
    "message": "Virtual Account List Retrieved",
    "data": {
        "accountNumber": "4050910184",
        "accountName": "Isaiah Falade",
        "bankCode": "000031",
        "bankName": "Premium Trust Bank",
        "accountType": "reserved",
        "accountStatus": "active",
        "expiryInMinutes": 0,
        "reference": "20250404000002",
        "createdAt": "2025-04-03T23:25:53"
    }
}
```

---

### Notes
- Ensure the `accountNumber` or `reference` provided is valid.
- Response data structure may change based on system updates.

