---
description: This api can be used to create an inquiry request for payout.
icon: message-dollar
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

# Inquiry

{% hint style="warning" %}
All inquiry requests will expire after 30 minutes, during which your funds will be temporarily locked.

The locked balance can be viewed under **Balance Histories > Reserved Balance.**
{% endhint %}

<mark style="color:green;">`POST`</mark> `/api/inquiry`

**Request**

<table><thead><tr><th width="191.73046875">Name</th><th width="84.48046875">Type</th><th width="92.765625" data-type="checkbox">Required</th><th width="176.0234375">Validation</th><th width="188.2265625">Description</th></tr></thead><tbody><tr><td>merchant_transaction_id</td><td>string</td><td>true</td><td></td><td>Unique identifier for the merchant's transaction.</td></tr><tr><td>bank_code</td><td>string</td><td>true</td><td></td><td>The bank code associated with the transaction.</td></tr><tr><td>amount</td><td>number</td><td>true</td><td>Required, Numeric,<br>Between 1 - 12 digits</td><td>The transaction amount is in numeric format.</td></tr><tr><td>account_number</td><td>string</td><td>true</td><td><p>Required, Numeric</p><p>Between 1 - 12 digits</p><p><br></p></td><td>The customer's account number for the transaction.</td></tr><tr><td>customer_name</td><td>string</td><td>true</td><td>Between 5 - 25 characters<br>Allowed chars: a-z, A-Z, 0-9, - (dash),(space)</td><td>The name of the customer associated with the transaction.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
    "merchant_transaction_id": "RP123456789",
    "amount": 100000,
    "bank_code": "014",
    "account_number": "0123456789",
    "customer_name": "John Doe"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

<table><thead><tr><th width="231.0546875">Name</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>Indicates whether the operation was successful <strong>true</strong> or not <strong>false</strong>.</td></tr><tr><td>data</td><td>Contains detailed information about the transaction.</td></tr><tr><td>data.merchant_transaction_id</td><td>Unique identifier for the merchant's transaction.</td></tr><tr><td>data.account_number</td><td>The account number associated with the transaction.</td></tr><tr><td>data.account_name</td><td>The name of the account holder (can be null if not available).</td></tr><tr><td>data.bank_code</td><td>The bank code associated with the transaction.</td></tr><tr><td>data.bank_name</td><td>The name of the bank handling the transaction.</td></tr><tr><td>data.amount</td><td>The transaction amount in numeric format.</td></tr><tr><td>data.fee</td><td>The transaction fee applied.</td></tr><tr><td>data.inquiry_id</td><td>Unique identifier for the transaction inquiry.</td></tr><tr><td>message</td><td>Contains information regarding the error message.</td></tr></tbody></table>

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "data": {
        "merchant_transaction_id": "RP123333333",
        "account_number": "0123456789",
        "account_name": "John Doe",
        "bank_code": "014",
        "bank_name": "PT. BANK CENTRAL ASIA, TBK.",
        "amount": 100000,
        "fee": 5500,
        "inquiry_id": "01jj1g751vqw68ng5546xnda5c"
    }
}
```
{% endtab %}

{% tab title="Failed" %}
```json
{
    "status":false,
    "data": null,
    "message":string,
}
```
{% endtab %}
{% endtabs %}
