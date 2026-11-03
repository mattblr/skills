---
name: app-store-release
description: Review an Apple app and prepare its App Store submission, metadata and verification evidence. Use for store readiness or submission work; submission itself requires user authorization.
---

# Prepare a reviewable App Store release

Start with the app's purpose, supported platforms/storefronts, data flows,
authentication and monetization. Read its delivery profile and current tracker.
Distinguish source inspection, a built app walkthrough, dashboard configuration,
and physical-device evidence. Report observed risks with file/flow references,
not automatic rejection claims based only on SDK imports or a URL.

Use current primary sources before applying policy:
- https://developer.apple.com/app-store/review/guidelines/
- https://developer.apple.com/help/app-store-connect/
- https://developer.apple.com/help/app-review/
- https://developer.apple.com/app-store/asset-best-practices/

Review only applicable categories, then record evidence and unresolved gates:

- Completeness: production endpoints, working reviewer access, no placeholders,
  crashes, hidden switches or unavailable promised features. Reviewer notes
  explain authentication and enabled paid functionality without public secrets.
- Social/UGC: terms, moderation, reporting, blocking, support contact and an
  operational response process. Exercise reporting and blocked-user exclusion;
  do not infer moderation works from a button or policy page alone.
- Privacy: specific permission purposes, denial paths, data minimization,
  account deletion initiation and completion, privacy policy, privacy manifests,
  required-reason APIs, third-party SDK practices and accurate App Privacy answers.
  Determine whether actual tracking requires ATT; first-party analytics alone
  is not evidence that ATT is required.
- Identity: applicable login alternatives and Apple identity continuity across
  native/web; fresh and returning users, account deletion and token revocation.
- Payments: applicable storefront rules and exceptions, StoreKit/RevenueCat
  products, subscription terms, restore, cancellation and server entitlement
  expiry. Do not universally prohibit external links without checking the rules
  for the selected storefront. Keep sandbox and live credentials separate.
- Presentation: correct layered/marketing icons, screenshots from the actual
  build, supported sizes and adaptive layouts, accessible controls, accurate
  age rating and metadata, licenses and ownership of supplied content.

Use mobile-app-verification for the runtime evidence and the provider's current
skills for purchase setup. Prepare archive/signing, metadata, screenshots,
review notes, compliance answers and a concise go/no-go checklist. Never invent
legal declarations, export-compliance answers, ratings or reviewer credentials.
Ask only for owner facts unavailable from the project/dashboard.

For any app that creates accounts, work through
[account deletion](references/account-deletion.md). Verify the whole flow rather
than accepting a settings button as evidence. Distinguish account closure,
background data erasure, third-party token revocation and subscription
cancellation. Report missing UGC safety controls as release gates even when the
app's principal feature works. Inspect the app's own required-reason API usage;
third-party privacy manifests do not cover the app's own calls.

For public posts, photos, comments or profiles, work through
[user-content safety](references/user-content-safety.md) and record runtime
evidence for filtering, reports, blocks and operator actions.

Do not present a release candidate or reusable template as complete while an
advertised feature is unfinished. Disabled switches, placeholder unavailability,
prepared code and local fixtures do not satisfy runtime/provider acceptance.
Report genuine external blockers with reproducible evidence and scope impact;
missing app credentials, grants or integration work are not automatically
platform failures. Keep submission/publication stopped until acceptance passes
or the owner explicitly decides the blocker's disposition. A known-gaps document
is not a waiver and does not authorize hiding promised functionality.

Upload and submission are distinct steps. Respect existing authorization; do
all reversible preparation and show the concrete release before requesting any
missing approval. Do not submit, release, accept agreements or change banking
without authorization. Record actual App Store Connect status after an allowed
submission, and keep review approval separate from readiness.

Starting-point credit: Safaiyeh's MIT-licensed
https://github.com/safaiyeh/app-store-review-skill informed the review categories.
These instructions are independently written; upstream claims and dates must
still be checked against Apple's current documentation.
