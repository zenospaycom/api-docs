---
description: This api can be used to check available balance.
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

# Check Balance

<mark style="color:green;">`GET`</mark> `/api/balance`

**Request**

{% tabs %}
{% tab title="Example Payload" %}
No payload needed
{% endtab %}
{% endtabs %}

***

**Response**

| Name                    | Description                                                               |
| ----------------------- | ------------------------------------------------------------------------- |
| status                  | Indicates whether the operation was successful **true** or not **false**. |
| data                    | Contains detailed information about the transaction.                      |
| data.balance            | The client's total account balance.                                       |
| data.reserved\_funds    | The client's total reserved funds.                                        |
| data.outstanding\_funds | The client's total outstanding funds.                                     |
| message                 | Contains information regarding the error message.                         |

{% tabs %}
{% tab title="Success" %}
```json
{
    "status": true,
    "data": {
        "balance": 528534207.52,
        "reserved_funds": 210000,
        "outstanding_funds": 0
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
