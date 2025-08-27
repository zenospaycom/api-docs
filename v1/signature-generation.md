---
icon: signature
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# Signature Generation

To generate signatures, you need an **RSA private and public key**. You can create these keys yourself or use a third-party tool such as [cryptotools.net](https://cryptotools.net/rsagen).

**Required Parameters**\
To create a valid signature, ensure the following parameters are included:

<table><thead><tr><th width="170.92578125">Parameter</th><th width="575.16796875">Description</th></tr></thead><tbody><tr><td>METHOD</td><td>The HTTP request method (e.g., <code>POST</code>, <code>GET</code>).</td></tr><tr><td>URL</td><td>The API endpoint URL (e.g., <code>/api/checkout</code>).</td></tr><tr><td>PAYLOAD</td><td>The <strong>SHA-256</strong> hash of the JSON request body, converted to a lowercase hexadecimal string. For <code>GET</code> requests, no payload needs to be sent.</td></tr><tr><td>TIMESTAMP</td><td>The current timestamp in <strong>ISO8601</strong> format.</td></tr><tr><td>SECRET_KEY</td><td>A unique shared key provided by the merchant.</td></tr></tbody></table>

#### **Concatenating Parameters**

#### The signature string (`stringToSign`) is formed by concatenating the parameters in the following format:

```
stringToSign = {METHOD}:{URL}:{PAYLOAD}:{TIMESTAMP}
```

Replace placeholders with actual values:

* `{METHOD}` → The HTTP request method.
* `{URL}` → The API endpoint URL (e.g., `/api/checkout`).
* `{PAYLOAD}` → The **SHA-256** hash of the JSON request body (no payload needs to be sent for `GET` requests).
* `{TIMESTAMP}` → The current timestamp in **ISO8601** format.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
const httpMethod = 'POST';
const endpointUrl = '/api/create/va';
const timestamp = '2024-12-16T12:11:14+07:00';
const payload = `
{
    "merchant_transaction_id": "ICZ10000001",
    "amount": "100000",
    "currency": "IDR",
    "bank_code": "nobu",
    "description": "Lorem Ipsum",
    "customer_name": "John Doe",
    "product_name": "Product Test"
}`;
const body = JSON.parse(payload);
const payload = crypto.createHash('sha256').update(JSON.stringify(body, null, 0)).digest('hex').toLowerCase();
const stringToSign = [
    httpMethod,
    endpointUrl,
    payload,
    timestamp
];
let signature = '';
const stringToSign = stringToSign.join(':');
const privateKey = fs.readFileSync('./path-to-private-key-file.pem');
const sign = crypto.createSign('RSA-SHA256');
sign.update(stringToSign);
signature = sign.sign(privateKey, 'base64');
console.log('Generated Signature:', signature);
```
{% endtab %}
{% endtabs %}

> * Ensure the private key is securely stored and not exposed in public repositories.
> * The `SECRET_KEY` should be kept **confidential** and used only for **authentication**.
> * The `TIMESTAMP` must be generated in **ISO8601** format and should not be more than a few minutes old to prevent replay attacks.
