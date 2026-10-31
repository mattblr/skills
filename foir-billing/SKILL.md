---
name: foir-billing
description: Set up or verify Stripe web and RevenueCat native billing for a Fóir-backed app, with shared identity and server-enforced entitlements. Use for provider setup, purchase reconciliation and billing release checks.
---

# Set up billing through scoped operations

Read the app's root config, operations, current provider adapters and project
profile before proposing changes. Discover OAuth Fóir tools, read served schemas,
and explicitly select environment/workspace/project/organization before writes.
Use current Stripe and RevenueCat skills/docs when available. Do not create a
second user pool or a frontend proxy with broader credentials.

Map both providers to the verified app actor. Define a provider-neutral private
subscription grant, its source/id, validity, revocation and quota relationship.
Keep free allowances separate. Enforce access in signed operations using the
verified ingress identity and dispatch-scoped data client; a client badge is
not proof of payment. Do not allow one provider's cancellation to revoke a
separate valid grant from another provider.

Review the exact grant table and supported operation contract before enabling
it. Store provider secrets in the credential mechanism the installed operation
can actually read; project secrets and app-install credentials may differ.
Never put secret keys in the client, public repo, command output or chat. Use
restricted sandbox keys, existing installation credentials and minimum provider
permissions. Preserve unrelated credentials when saving a form.

Stripe: use the app's signed Checkout/Portal operations and configured product,
price, currency, interval and return origins. Bind customer/subscription mapping
to the verified actor, not a browser-supplied user ID. Validate webhook signature
against raw bytes, persist deduplication/ordering state, fetch authoritative
provider state, and reconcile grants idempotently. RevenueCat: identify the same
actor, verify active entitlements server-side and reconcile restore/renewal/
expiration/refund/cancellation into the same grant mechanism.

Prefer Fóir's supported awaited continuation/queue semantics for long work.
Do not introduce an external queue before checking that contract. Never rely on
an unobserved promise after returning. If a platform primitive is missing,
document current behavior and intended replacement beside the adapter; do not
promise that future native payments also replace app-specific quotas.

Prove in an isolated sandbox: unpaid Checkout/Portal; simulated purchase;
refresh/restore and shared web/native entitlement; partial/full refund;
cancel-at-period-end and expiry; renewal; duplicate/out-of-order delivery;
invalid signature; wrong actor; expired dispatch; retry/recovery after failure.
Record which outcomes were actually observed and which are fixtures. Do not
count gateway acknowledgment alone as proof a consumer completed successfully.
Use test transactions only within approved scope; hand off any action the tool's
approval policy requires the user to perform.

Keep billing disabled by default until acceptance, production credentials,
webhook routing and live activation are explicitly authorized. Provide exact
rollback and leave existing subscriptions intact during hosting changes.
