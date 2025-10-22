---
description: >-
  This API allows merchants to generate a checkout page for transaction
  processing.
icon: building-columns
---

# Bank Account

`POST` `/api/create/bank`

**Request**

| Name                      |   Type | Required | Validation                                                                 | Description                                                |
| ------------------------- | -----: | :------: | -------------------------------------------------------------------------- | ---------------------------------------------------------- |
| merchant\_transaction\_id | string |   true   |                                                                            | Unique identifier for the merchant's transaction.          |
| amount                    | string |   true   | Numeric, 1-12 digits                                                       | The transaction amount in numeric format.                  |
| currency                  | string |   true   | **Allowed value:** `"IDR"`                                                 | The currency for the transaction (Indonesian Rupiah only). |
| bank\_code                | string |   true   | Allowed value: BCA, MDR, BNI, BRI                                          | The bank code for the transaction                          |
| customer\_name            | string |   true   | Between 5 - 25 characters. Allowed chars: a-z, A-Z, 0-9, - (dash), (space) | Name of the customer associated with the transaction.      |
| product\_name             | string |   true   | Between 5 - 25 characters. Allowed chars: a-z, A-Z, 0-9, - (dash), (space) | Name of the product associated with the transaction.       |
| description               | string |   false  |                                                                            | Additional details about the transaction.                  |

{% tabs %}
{% tab title="Example Payload" %}
```json
{
    "merchant_transaction_id": "ICZ10000001",
    "amount": "100000",
    "currency": "IDR",
    "bank_code": "BCA",
    "description": "Lorem Ipsum",
    "customer_name": "John Doe",
    "product_name": "Product Test"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

| Name                 | Description                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| status               | Indicates the status of the request. **true** if successful, **false** otherwise.                                        |
| message              | A message describing the result of the request. Typically "success" if the request was successful.                       |
| data.account\_number | The generated bank account number. This number is used by the customer to make the payment.                              |
| data.account\_name   | The name of the account holder.                                                                                          |
| data.amount          | The total amount the user must transfer.                                                                                 |
| data.channel         | The bank or payment channel associated with the Bank Account Payment                                                     |
| data.redirect\_url   | A URL to which the user should be redirected (if applicable). This field may be **null** if no redirect URL is provided. |

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "message": "success",
    "data": {
        "account_number": "4871002066",
        "account_name": "John Doe",
        "amount": 100089,
        "channel": "BANK_BCA",
        "redirect_url": "{host}/checkout/9e536777-2bfa-4161-9931-35f5c4b23faf/bank/BCA"
    }
}
```
{% endtab %}

{% tab title="Failed" %}
```json
{
    "status": false,
    "message": string
}
```
{% endtab %}
{% endtabs %}

***

**Callback**

{% hint style="warning" %}
To receive a callback, you must first **register** your domain URL.

The callback is triggered only after the user **completes the payment**.
{% endhint %}

`POST` `{your_callback_url}`

| Name                          | Description                                                             |
| ----------------------------- | ----------------------------------------------------------------------- |
| transaction\_id               | Unique identifier for the transaction.                                  |
| merchant\_transaction\_id     | Unique identifier provided by the client for the merchant               |
| created\_at                   | Timestamp when the transaction was created.                             |
| amount                        | Total transaction amount.                                               |
| currency                      | Currency used in the transaction (e.g., IDR, USD).                      |
| channel                       | Payment channel used (e.g., BCA, QRIS).                                 |
| service\_fee\_rate            | Service fee percentage applied (e.g., 2.5, 3.0).                        |
| service\_fee\_amount          | Total service fee deducted (e.g., 2000, 4000).                          |
| nett\_amount                  | Final amount received after fee deductions.                             |
| rrn                           | RRN (Retrieval Reference Number) of the associated payment transaction. |
| customer\_info                | Additional customer details.                                            |
| customer\_info.customer\_name | Customer's name.                                                        |
| customer\_info.product\_name  | Product name associated with the transaction.                           |

{% tabs %}
{% tab title="Example Payload" %}
```json
{
  "transaction_id": "9dc1614d-ed70-426c-80da-5304ad258c9c",
  "merchant_transaction_id": "RLP0000000000",
  "created_at": "2024-12-18T16:21:07.000000Z",
  "amount": "10000.00",
  "currency": "IDR",
  "channel": "BCA",
  "service_fee_rate": 0,
  "service_fee_amount": 0,
  "nett_amount": 10000,
  "rrn": null,
  "customer_info": {
       "customer_name": "John Doe",
       "product_name": "Deposit Now"
  }
}
```
{% endtab %}
{% endtabs %}
