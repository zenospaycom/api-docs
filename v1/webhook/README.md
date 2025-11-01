---
description: >-
  The system sends webhook notifications to your registered callback URL when
  important events occur. You must configure your webhook endpoint during client
  onboarding or through the admin panel.
icon: anchor
---

# Webhook

### Webhook Registration

Webhook endpoints are registered during client onboarding or can be configured later through the admin panel. Each event type requires a separate webhook configuration with:

* Base URL (e.g., https://yourdomain.com)
* Path (e.g., /api/webhooks/payment)

The full webhook URL is constructed as: {base\_url}{path}

### Response Requirements

Your webhook endpoint should respond with a standard HTTP status code:

* 200-299: Success (webhook processed successfully)
* 4xx: Client error (will not be retried)
* 5xx: Server error (will be retried)

Response time should be under 2 seconds to avoid timeout. The webhook system has a 2-second timeout.

### Security Best Practices

1. Always verify the X-SIGNATURE header to authenticate the request
2. Verify the X-PARTNER-ID matches your client ID
3. Check the X-TIMESTAMP to prevent replay attacks
4. Use HTTPS for your webhook endpoint
5. Implement idempotency checks using transaction IDs to prevent duplicate processin
