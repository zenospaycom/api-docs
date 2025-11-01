---
icon: anchor-circle-check
---

# Disbursement Completed Webhook

<mark style="color:green;">`POST`</mark> `disbursement.completed`

**Payload Structure**

| Name                           | Type   | Description                                               |
| ------------------------------ | ------ | --------------------------------------------------------- |
| event                          | string | Event name: "disbursement.completed"                      |
| data                           | object | Disbursement detail                                       |
| data.id                        | string | Inquiry ID (unique identifier)                            |
| data.merchant\_transaction\_id | string | Unique identifier provided by the client for the merchant |
| data.amount                    | number | Total transaction amount.                                 |
| data.bank\_code                | string | Bank code (e.g., "014", "002")                            |
| data.bank\_name                | string | Full bank name                                            |
| data.account\_name             | string | Recipient account holder name                             |
| data.account\_number           | string | Recipient account number                                  |
| data.status                    | string | Status: "success" or "fail"                               |
| data.created\_at               | string | Inquiry creation timestamp (ISO 8601)                     |
| data.updated\_at               | string | Last update timestamp (ISO 8601)                          |

```json
{
  "event": "disbursement.completed",
  "data": {
    "id": "01jmmtbfcthj8y0eg3w1he4q3t",
    "merchant_transaction_id": "RLG00000000",
    "amount": 25000,
    "bank_code": "002",
    "bank_name": "Bank Rakyat Indonesia",
    "account_name": "John Doe",
    "account_number": "0000000000",
    "status": "success",
    "created_at": "2025-01-10T00:54:42+07:00",
    "updated_at": "2025-01-10T00:54:48+07:00"
  }
}
```
