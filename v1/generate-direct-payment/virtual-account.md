---
description: >-
  This API allows merchants to generate a checkout page for transaction
  processing.
hidden: true
icon: vr-cardboard
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

# Virtual Account

<mark style="color:green;">`POST`</mark> `/api/create/va`

**Request**

<table><thead><tr><th width="212.08984375">Name</th><th width="80.859375">Type</th><th data-type="checkbox">Required</th><th>Validation</th><th width="185.125">Description</th></tr></thead><tbody><tr><td>merchant_transaction_id</td><td>string</td><td>true</td><td></td><td>Unique identifier for the merchant's transaction.</td></tr><tr><td>amount</td><td>string</td><td>true</td><td>Numeric, 1-12 digits</td><td>The transaction amount in numeric format.</td></tr><tr><td>currency</td><td>string</td><td>true</td><td><strong>Allowed value:</strong> <code>"IDR"</code></td><td>The currency for the transaction (Indonesian Rupiah only).</td></tr><tr><td>bank_code</td><td>string</td><td>true</td><td>Allowed value: NOBU</td><td>The bank code for the transaction</td></tr><tr><td>customer_name</td><td>string</td><td>true</td><td><p>Between 5 - 25 characters</p><p>Allowed chars: a-z, A-Z, 0-9, - (dash),(space)</p></td><td>Name of the customer associated with the transaction.</td></tr><tr><td>product_name</td><td>string</td><td>true</td><td><p>Between 5 - 25 characters</p><p>Allowed chars: a-z, A-Z, 0-9, - (dash),(space)</p></td><td>Name of the product associated with the transaction.</td></tr><tr><td>description</td><td>string</td><td>false</td><td></td><td>Additional details about the transaction.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
    "merchant_transaction_id": "ICZ10000001",
    "amount": "100000",
    "currency": "IDR",
    "bank_code": "BRI",
    "description": "Lorem Ipsum",
    "customer_name": "John Doe",
    "product_name": "Product Test"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

<table><thead><tr><th width="205.48828125">Name</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>Indicates the status of the request. <strong>true</strong> if successful, <strong>false</strong> otherwise.</td></tr><tr><td>message</td><td>A message describing the result of the request. Typically "success" if the request was successful.</td></tr><tr><td>data.va_number</td><td>The generated Virtual Account (VA) number. This number is used by the customer to make the payment. This field may be empty if no virtual account number is provided.</td></tr><tr><td>data.channel</td><td>The bank or payment channel associated with the Virtual Account.</td></tr><tr><td>data.redirect_url</td><td>A URL to which the user should be redirected (if applicable). This field may be <mark style="color:orange;"><strong>null</strong></mark> if no redirect URL is provided.</td></tr></tbody></table>

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "message": "success",
    "data": {
        "va_number": "8999817535253527",
        "channel": "MDR",
        "redirect_url": "{host}/checkout/9e536777-2bfa-4161-9931-35f5c4b23faf/va/MDR"
    }
}
```
{% endtab %}

{% tab title="Failed" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>    "status": false,
    "message": string,
}
</code></pre>
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
  "rrn": null,
  "customer_info": {
       "customer_name": "John Doe",
       "product_name": "Deposit Now"
  }
}
```
{% endtab %}
{% endtabs %}
