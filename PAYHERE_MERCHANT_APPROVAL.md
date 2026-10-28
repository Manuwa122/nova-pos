# PayHere merchant approval checklist — NovaPOS

**Status: Application not submitted; live payments disabled.**

## 1. Merchant onboarding
- Visit https://www.payhere.lk/ and register / verify email.
- Complete Activation Form with accurate business and beneficial-owner information.
- Select business type: registered company, sole proprietorship, partnership, home business, freelance, etc.
- Upload PayHere-requested identity/business proof and bank account verification.
- Sign merchant agreement as required for the selected entity.
- Await bank partner review. PayHere guidance: roughly 1–3 days, not guaranteed.
- Approval belongs to PayHere / partner bank; NovaPOS cannot approve accounts.

## 2. Website approval readiness
- Replace any sample products with genuine goods/services, correct prices and availability.
- Publish **accurate** business name, physical/postal address, email and phone number.
- Publish actual business Terms, Privacy Policy and Return/Refund Policy.
- Remove demo-only claims from any merchant-facing sales website.
- Ensure site is accessible with HTTPS and goods are genuinely purchasable.
- Do not invent personal or business data, refund policies, or legal claims.

## 3. PayHere API approval
- After merchant approval: PayHere Dashboard > Integrations > Add Domain/App.
- Register the domain used for payment requests; for this project use nova-pos-4tta.vercel.app unless moving to a custom domain.
- Request domain approval, then obtain the Merchant ID and domain-specific Merchant Secret.
- **Never paste Merchant Secret into browser settings, GitHub issues, source code, README, or chat.** Store it in encrypted Vercel server environment variables.

## 4. Required architecture before accepting live payments
- Server-side database to persist authoritative orders and payment attempts.
- Server endpoint to create a pending order, reprice against trusted inventory, and calculate PayHere hash privately.
- Hosted PayHere payment redirect / SDK using generated, signed fields.
- Public server-side notification endpoint receiving application/x-www-form-urlencoded data.
- Validate merchant ID, order ID, expected amount/currency, status and signature with constant-time comparison.
- Idempotently mark paid only for valid verified status_code=2. Keep records of failures, cancels and chargebacks.
- Client return_url is **not** payment proof. Browser polls verified status from backend.
- Do not decrement inventory, send paid receipts or record revenue before verified settlement callback.
- Test sandbox success, failure, cancellation, replayed/mismatched callbacks, and concurrent stock changes.

Docs: https://support.payhere.lk/application-process
Checkout API: https://support.payhere.lk/api-%26-mobile-sdk/checkout-api

## 5. Current NovaPOS limitations
NovaPOS currently stores sales and inventory in browser localStorage. This is not safe as the authoritative state for online payment orders. No live PayHere connection exists and no test transaction has been run.

## 6. Owner follow-up
Confirm business type, approval state, real product catalog, public business contact information, and approved merchant domain. Merchant credentials must be added directly to Vercel, never sent over chat.
