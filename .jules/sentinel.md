## 2024-11-07 - Insecure Direct Object Reference in Payment Verification
**Vulnerability:** `app/api/payment/verify/route.ts` used a fallback to client-provided `orderId` if the Stripe Payment Intent metadata `order_id` was missing. This allowed marking arbitrary orders as paid.
**Learning:** Never trust client-provided IDs for authorization when a verified server-side source (like Stripe metadata) is available. Bypassing metadata checks enables IDOR.
**Prevention:** Strictly enforce that the intent metadata ID matches the requested ID and reject mismatched or missing data.
