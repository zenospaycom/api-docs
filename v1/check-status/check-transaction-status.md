---
description: >-
  This API can be used to check the status of a transaction. When the rrn
  parameter is specified, it will take priority in the search.
icon: hourglass-clock
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

# Check Transaction Status

<mark style="color:green;">`POST`</mark> `/api/check/transaction`

**Request**

<table><thead><tr><th width="212.08984375">Name</th><th width="69.63671875">Type</th><th width="94.1953125" data-type="checkbox">Required</th><th width="373.05078125">Description</th></tr></thead><tbody><tr><td>merchant_transaction_id</td><td>string</td><td>false</td><td>Unique identifier for the merchant's transaction.</td></tr><tr><td>rrn</td><td>string</td><td>false</td><td>RRN (Retrieval Reference Number) of the associated payment transaction.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
  "merchant_transaction_id": "ICZ10000001",
  "rrn": "015221245517"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

<table><thead><tr><th width="259.9453125">Name</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>Indicates the status of the request. <strong>true</strong> if successful, <strong>false</strong> otherwise.</td></tr><tr><td>data.status</td><td>The current status of the transaction (e.g., <mark style="color:green;">Success</mark>, <mark style="color:yellow;">Pending</mark>, <mark style="color:red;">Fail</mark>)</td></tr><tr><td>data.transaction_id</td><td>The unique identifier for the transaction provided by the merchant.</td></tr><tr><td>data.merchant_transaction_id</td><td>The unique identifier of the merchant's transaction.</td></tr><tr><td>data.amount</td><td>The numeric value of the transaction amount.</td></tr><tr><td>data.channel</td><td>The payment channel used for the transaction.</td></tr><tr><td>data.created_at</td><td>The timestamp when the transaction was created.</td></tr><tr><td>data.updated_at</td><td>The timestamp when the transaction was last updated.</td></tr><tr><td>data.service_fee_rate</td><td>The percentage fee applied to the transaction.</td></tr><tr><td>data.service_fee_amount</td><td>The fixed service fee amount deducted from the transaction.</td></tr><tr><td>data.service_fee_final</td><td>The transaction fee applied.</td></tr><tr><td>data.nett_amount</td><td>The final amount credited to the merchant after deducting fees.</td></tr><tr><td>data.rrn</td><td>RRN (Retrieval Reference Number) of the associated payment transaction.</td></tr></tbody></table>

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "data": {
        "status": "Success",
        "transaction_id": "0aa59d5a-2a10-45be-a174-f7b954113d12",
        "created_at": "2025-01-01T00:00:00.000000Z",
        "updated_at": "2025-01-01T12:00:00.000000Z",
        "merchant_transaction_id": "INQ12300456",
        "amount": "100000.00",
        "channel": "QRIS",
        "service_fee_rate": "4",
        "service_fee_amount": "0",
        "service_fee_final": "2000",
        "nett_amount": "96000",
        "rrn": "987654321"
    }
}
```
{% endtab %}

{% tab title="Failed" %}
```json
{
    "status": false,
    "data": null
    "message": string
}
```
{% endtab %}
{% endtabs %}
