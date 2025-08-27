---
description: This API can be used to check the status of an inquiry
icon: hourglass-clock
---

# Check Inquiry Status

<mark style="color:green;">`POST`</mark> `/api/check/inquiry`

**Request**

<table><thead><tr><th width="212.08984375">Name</th><th width="76.2421875">Type</th><th width="88.7265625" data-type="checkbox">Required</th><th width="363.32421875">Description</th></tr></thead><tbody><tr><td>merchant_transaction_id</td><td>string</td><td>true</td><td>Unique identifier for the merchant's transaction.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example Payload" %}
```json
{
  "merchant_transaction_id": "ICZ10000001"
}
```
{% endtab %}
{% endtabs %}

***

**Response**

<table><thead><tr><th width="259.9453125">Name</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>Indicates the status of the request. <strong>true</strong> if successful, <strong>false</strong> otherwise.</td></tr><tr><td>data.status</td><td>The current status of the transaction (e.g., <mark style="color:green;">Success</mark>, <mark style="color:yellow;">Pending</mark>, <mark style="color:purple;">Processing</mark>, <mark style="color:red;">Fail</mark>)</td></tr><tr><td>data.merchant_transaction_id</td><td>Unique identifier of the merchant's transaction.</td></tr><tr><td>data.amount</td><td>The numeric value of the transaction amount.</td></tr><tr><td>data.bank_code</td><td>The code representing the bank associated with the transaction.</td></tr><tr><td>data.account_number</td><td>The account number used for the transaction.</td></tr><tr><td>data.reason</td><td>The reason for the transaction failure or status update (nullable).</td></tr><tr><td>data.service_fee_final</td><td>The transaction fee applied.</td></tr></tbody></table>

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "data": {
        "status": "success",
        "created_at": "2025-01-01T00:00:00.000000Z",
        "updated_at": "2025-01-01T12:00:00.000000Z",
        "merchant_transaction_id": "INQ12300456",
        "amount": "100000.00",
        "bank_code": "009",
        "account_number": "00000000",
        "reason": "",
        "service_fee_final": "5500.00"
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
