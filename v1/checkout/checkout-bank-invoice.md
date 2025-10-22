---
description: This API allows you to generate a checkout page for Line Bank transfers.
icon: file-invoice-dollar
---

# Checkout Bank Invoice

`POST` `/api/checkout/bank`

**Request**

| Name                      |   Type | Required | Validation                                        | Description                                                |
| ------------------------- | -----: | :------: | ------------------------------------------------- | ---------------------------------------------------------- |
| merchant\_transaction\_id | string |   true   |                                                   | Unique identifier for the merchant's transaction.          |
| amount                    | string |   true   | Numeric, 1-12 digits                              | The transaction amount in numeric format.                  |
| currency                  | string |   true   | **Allowed value:** `"IDR"`                        | The currency for the transaction (Indonesian Rupiah only). |
| customer\_name            | string |   true   | 5-25 characters, Allowed: `a-z A-Z 0-9 - (space)` | Name of the customer associated with the transaction.      |
| product\_name             | string |   true   | 5-25 characters, Allowed: `a-z A-Z 0-9 - (space)` | Name of the product associated with the transaction.       |
| description               | string |   false  |                                                   | Additional details about the transaction.                  |

{% tabs %}
{% tab title="Example Payload" %}
```json
{
  "merchant_transaction_id": "ICZ10000001",
  "amount": "100000",
  "currency": "IDR",
  "description": "Lorem Ipsum",
  "customer_name": "John Doe",
  "product_name": "Product Test"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

| Name                             | Description                                                                |
| -------------------------------- | -------------------------------------------------------------------------- |
| transaction\_id                  | The unique identifier for the transaction provided by the merchant.        |
| client\_id                       | The requestor client id                                                    |
| amount                           | The numeric value of the transaction amount.                               |
| currency                         | The currency used for the transaction. Only IDR is supported.              |
| description                      | The description that describes the transaction.                            |
| customer\_details                | The customer details involved in the transaction.                          |
| customer\_details.customer\_name | The customer name involved in the transaction                              |
| customer\_details.product\_name  | The product name involved in the transaction                               |
| checkout\_url                    | A web URL for redirecting users to complete the payment via a web browser. |

{% tabs %}
{% tab title="Success" %}
```json
{
    "transaction_id": "9e536777-2bfa-4161-9931-35f5c4b23faf",
    "client_id": "9dbf86be-f9e9-4000-8b39-fdd5a841fce1",
    "amount": "100000",
    "currency": "IDR",
    "description": "Order Product",
    "customer_details": "{\"customer_name\":\"John Doe\",\"product_name\":\"Product Test\"}",
    "checkout_url": "{host}/checkout/9e536777-2bfa-4161-9931-35f5c4b23faf"
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
