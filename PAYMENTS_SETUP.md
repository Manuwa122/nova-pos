# Real payments setup — NovaPOS

## Current status
**Live payment processing is NOT activated.** The checkout currently records externally confirmed payments only. Never ask buyers to enter card data inside NovaPOS.

## Recommended initial provider: PayHere (Sri Lanka)
Official integration documentation: https://support.payhere.lk/api-%26-mobile-sdk/checkout-api

1. Obtain an approved PayHere merchant account.
2. Register the production domain `nova-pos-4tta.vercel.app` (or your custom domain) with PayHere and obtain its domain-specific merchant secret.
3. Provision a persistent server-side database for orders, payment attempts, status, and idempotent webhook events. The current browser localStorage is **not** an authoritative order store.
4. Implement a Vercel server endpoint to create a pending order, recompute prices/tax from trusted catalog data, and generate the PayHere checkout hash server-side.
5. Never expose the PayHere merchant secret to JavaScript, GitHub, or browser localStorage. Configure it in Vercel server environment variables.
6. Implement a public notification endpoint that checks merchant ID, amount, currency, expected order, and PayHere MD5 signature; use constant-time comparison, idempotent transaction updates and atomic inventory updates. Treat only verified status_code=2 as paid; handle failure/pending/refund/chargeback.
7. Return URL / browser popup success **must not** finalize the sale. Poll server order status instead.
8. Test sandbox successes, failures, cancellations, duplicate callbacks, mismatched amount/currency, refreshes, retries, and stock conflicts before switching to live credentials.
9. Only then enable the live checkout button and receipts for verified payments.

Checkout endpoint: `https://www.payhere.lk/pay/checkout`
Sandbox endpoint: `https://sandbox.payhere.lk/pay/checkout`

## Required from the owner
- Which approved gateway and merchant account: PayHere / WEBXPAY / OnePay / other?
- Has the production domain been registered/approved with the provider?
- A database provider/connection configured securely in Vercel (do not send secrets in chat).

Do not put payment gateway credentials in NovaPOS Settings. A public Merchant ID may be shown, but secret values belong only in Vercel environment configuration.

## Supported payment types
Available card brands, wallet types, and QR networks depend on the merchant's provider plan and the provider's current capabilities. A generic gateway selector does not imply support for every payment method.
