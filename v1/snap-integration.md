---
icon: handshake
---

# Snap Integration

### Explanation

Snap is a payment method that allows you to create a seamless checkout experience. To interact with the Snap service, you need to **include specific headers in each request**. These headers help our system validate and process your transactions.

### Required Headers

To ensure transaction security, **SNAP API** uses security standards established by Bank Indonesia by employing **signature** and **encryption**.

We use the **Asymmetric Without Get Token** type to generate the signature; therefore, merchants **do not** need to make an additional get token request to create the signature. This signature is sent via the X-Signature header when making a request. In addition to X-Signature, **the required headers that must be sent** with your request are:

| Header       | Description                                                                   |
| ------------ | ----------------------------------------------------------------------------- |
| X-TIMESTAMP  | The current timestamp in **ISO8601** format (e.g., 2024-12-19T17:07:05+07:00) |
| X-SIGNATURE  | Merchant generated signature                                                  |
| X-PARTNER-ID | Client key given to the merchant                                              |
