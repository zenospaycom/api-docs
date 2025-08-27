---
description: >-
  This API allows merchants to generate a checkout page for transaction
  processing.
icon: file-lines
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# Checkout Invoice

<mark style="color:green;">`POST`</mark> `/api/checkout`

**Request**

<table><thead><tr><th width="212.65625">Name</th><th width="82.26953125">Type</th><th width="84.35546875" data-type="checkbox">Required</th><th>Validation</th><th width="223.890625">Description</th></tr></thead><tbody><tr><td>merchant_transaction_id</td><td>string</td><td>true</td><td></td><td>Unique identifier for the merchant's transaction.</td></tr><tr><td>amount</td><td>string</td><td>true</td><td>Numeric, 1-12 digits</td><td>The transaction amount in numeric format.</td></tr><tr><td>currency</td><td>string</td><td>true</td><td><strong>Allowed value:</strong> <code>"IDR"</code></td><td>The currency for the transaction (Indonesian Rupiah only).</td></tr><tr><td>customer_name</td><td>string</td><td>true</td><td>5-25 characters, Allowed: <code>a-z A-Z 0-9 - (space)</code></td><td>Name of the customer associated with the transaction.</td></tr><tr><td>product_name</td><td>string</td><td>true</td><td>5-25 characters, Allowed: <code>a-z A-Z 0-9 - (space)</code></td><td>Name of the product associated with the transaction.</td></tr><tr><td>description</td><td>string</td><td>false</td><td></td><td>Additional details about the transaction.</td></tr></tbody></table>

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

<table><thead><tr><th width="329.98828125">Name</th><th>Description</th></tr></thead><tbody><tr><td>transaction_id</td><td>The unique identifier for the transaction provided by the merchant.</td></tr><tr><td>client_id</td><td>The requestor client id</td></tr><tr><td>amount</td><td>The numeric value of the transaction amount.</td></tr><tr><td>currency</td><td>The currency used for the transaction. Only IDR is supported.</td></tr><tr><td>description</td><td>The description that describes the transaction.</td></tr><tr><td>customer_details</td><td>The customer details involved in the transaction.</td></tr><tr><td>customer_details.customer_name</td><td>The customer name involved in the transaction</td></tr><tr><td>customer_details.product_name</td><td>The product name involved in the transaction</td></tr><tr><td>checkout_url</td><td>A web URL for redirecting users to complete the payment via a web browser.</td></tr></tbody></table>

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

{% tab title="Failed" %}
```
{
    "status":false,
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

<mark style="color:green;">`POST`</mark> `{your_callback_url}`

<table><thead><tr><th width="269.14453125">Name</th><th>Description</th></tr></thead><tbody><tr><td>transaction_id</td><td>Unique identifier for the transaction.</td></tr><tr><td>merchant_transaction_id</td><td>Unique identifier provided by the client for the merchant</td></tr><tr><td>created_at</td><td>Timestamp when the transaction was created.</td></tr><tr><td>amount</td><td>Total transaction amount.</td></tr><tr><td>currency</td><td>Currency used in the transaction (e.g., IDR, USD).</td></tr><tr><td>channel</td><td>Payment channel used (e.g., BCA, QRIS).</td></tr><tr><td>service_fee_rate</td><td>Service fee percentage applied (e.g., 2.5, 3.0).</td></tr><tr><td>service_fee_amount</td><td>Total service fee deducted (e.g., 2000, 4000).</td></tr><tr><td>nett_amount</td><td>Final amount received after fee deductions.</td></tr><tr><td>rrn</td><td>RRN (Retrieval Reference Number) of the associated payment transaction.</td></tr><tr><td>customer_info</td><td>Additional customer details.</td></tr><tr><td>customer_info.customer_name</td><td>Customer's name.</td></tr><tr><td>customer_info.product_name</td><td>Product name associated with the transaction.</td></tr></tbody></table>

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
  "rrn": "987654321",
  "customer_info": {
       "customer_name": "John Doe",
       "product_name": "Deposit Now"
  }
}

```
{% endtab %}
{% endtabs %}
