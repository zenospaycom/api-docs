---
description: >-
  To receive a callback, you must first register your domain URL.  The callback
  is triggered only after the user completes the payment.
icon: anchor-circle-check
---

# Payment Completed Webhook

{% hint style="warning" %}
To receive a callback, you must first **register** your domain URL.

The callback is triggered only after the user **completes the payment**.
{% endhint %}

<mark style="color:green;">`POST`</mark>`payment.completed`   &#x20;

**Payload Structure**

| Name                      | Type        | Description                                                  |
| ------------------------- | ----------- | ------------------------------------------------------------ |
| transaction\_id           | string      | Internal transaction identifier                              |
| merchant\_transaction\_id | string      | Unique identifier for the merchant's transaction.            |
| created\_at               | string      | Transaction creation timestamp (ISO 8601)                    |
| amount                    | number      | Transaction amount                                           |
| currency                  | string      | The currency for the transaction (Indonesian Rupiah only).   |
| channel                   | string      | Payment Channel                                              |
| service\_fee\_rate        | number      | Service fee rate applied                                     |
| service\_fee\_amount      | number      | Service fee amount charged                                   |
| nett\_amount              | number      | Net amount after fees                                        |
| rrn                       | string/null | Retrieval Reference Number (if available)                    |
| customer\_info            | object      | Customer information object (decoded from customer\_details) |

**Example Payload**

{% tabs %}
{% tab title="Success" %}
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
  "rrn": "0392813042",
  "customer_info": {
       "customer_name": "John Doe",
       "product_name": "Deposit Now"
  }
}
```
{% endtab %}
{% endtabs %}

