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


### Response Fields
| Field | Type | Description | Nullable |
|-------|------|-------------|----------|
| status | Boolean | Request success status | No |
| message | String | Response message | No |
| data | Object | Virtual account details | No |
| data.accountNumber | String | Virtual account number | No |
| data.accountName | String | Name associated with the account | No |
| data.bankCode | String | Bank identifier code | No |
| data.bankName | String | Name of the bank | No |
| data.accountType | String | Type of virtual account (e.g., "reserved") | No |
| data.accountStatus | String | Current status of the account | No |
| data.expiryInMinutes | Number | Minutes until account expiry (0 for non-expiring) | No |
| data.reference | String | Unique reference identifier | No |
| data.createdAt | String | ISO 8601 timestamp of account creation | No |


---

### Notes
- Ensure the `accountNumber` or `reference` provided is valid.
- Response data structure may change based on system updates.

