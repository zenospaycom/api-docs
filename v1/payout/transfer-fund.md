---
description: This API can be used to transfer funds using the specified inquiry ID
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

# Transfer fund

{% hint style="warning" %}
Please note that a response status of "true" **does not indicate** that the disbursement was successful.
{% endhint %}

<mark style="color:green;">`POST`</mark> `/api/transfer`

**Request**

<table><thead><tr><th width="116.26171875">Name</th><th width="86.8671875">Type</th><th width="86.453125" data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td>inquiry_id</td><td>string</td><td>true</td><td>Unique identifier for the inquiry to be processed</td></tr><tr><td>force</td><td>bool</td><td>false</td><td><p>If <strong>true</strong>, transfer will be initiated regardless of account validity.</p><p>Default: <strong>false</strong></p></td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
    "inquiry_id": "01jj1g751vqw68ng5546xnda5c",
    "force": true
}
```
{% endtab %}
{% endtabs %}

***

**Response**

| Name    | Description                                                              |
| ------- | ------------------------------------------------------------------------ |
| status  | Indicates whether the operation was successful **true** or not **false** |
| message | Contains information regarding the error message.                        |

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true
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

To receive a callback, you must register your domain url first. This callback will only be sent after the disbursement process **has been completed.**
{% endhint %}



_A request will be sent to the path:_

<mark style="color:green;">`POST`</mark> `{your_callback_url}`

<table><thead><tr><th width="264.64453125">Name</th><th>Description</th></tr></thead><tbody><tr><td>event</td><td>The event name that triggered the web-hook (e.g., disbursement.completed, payment.completed).</td></tr><tr><td>data</td><td>The data object contains the disbursement details.</td></tr><tr><td>data.id</td><td>Inquiry ID unique identifier</td></tr><tr><td>data.merchant_transaction_id</td><td>The transaction ID provided by the merchant for this disbursement.</td></tr><tr><td>data.amount</td><td>The amount of the disbursement.</td></tr><tr><td>data.bank_code</td><td>The bank code for the payment processor (e.g., 014, 002).</td></tr><tr><td>data.account_name</td><td>The name of the account holder receiving the disbursement.</td></tr><tr><td>data.account_number</td><td>The account number of the recipient.</td></tr><tr><td>data.status</td><td>The current status of the disbursement (e.g., success, pending, fail).</td></tr><tr><td>data.created_at</td><td>The timestamp when the disbursement was created (ISO 8601 format).</td></tr><tr><td>data.updated_at</td><td>The timestamp when the disbursement was last updated (ISO 8601 format).</td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
  "event": "disbursement.completed",
  "data": {
    "id": "01jmmtbfcthj8y0eg3w1he4q3t",
    "merchant_transaction_id": "RLG00000000",
    "amount": "25000.00",
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
{% endtab %}
{% endtabs %}
