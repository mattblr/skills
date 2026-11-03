---
name: build-foir-app
description: Implement the planned tickets for a Fóir-backed iOS/web subscription app and embedded admin console, preserving the template framework and using native Fóir features for backend infrastructure. Use after discovery and refactor planning.
---

# Build the planned app

Read the product brief, refactor matrix, epic/ticket dependencies, settled
choices, AGENTS.md, root config and delivery profile. Follow the bundled
turtleneck Deliver/Track workflow for implementation and evidence. Start with
an unblocked planned ticket and keep the tracker current. If no plan exists,
use plan-foir-app first; do not invent a different product or repeat discovery.

## Framework and platform contract

Preserve the iOS app, web app/website, subscription purchase/restore and shared
server-enforced entitlement integration, plus the admin console embedded in
Fóir. Keep shared identity, hosted-session handling, CMS/editable copy/tokens,
build/codegen/deployment setup and existing Fóir feature integrations. Adapt
application-specific models, screens, rules, paid benefits, content and branding
as the tickets specify. Do not discard framework pieces because their example
mentions the old domain. A free launch leaves commercial experiences inactive
while retaining subscription support. Respect explicit scope changes recorded
in the plan; do not infer permission for them from an unrelated app idea.

Before introducing backend work, discover the current Fóir MCP tools and served
schemas, select the user's workspace/project/environment/organization explicitly,
and read the served no-backend and app-architecture guidance. Use Fóir's native
identity/auth, access control, data/files, quotas/entitlements, notifications,
hooks/schedules and queued execution. Only application-specific business logic
belongs in operation handlers. Never implement app-owned metering, ledgers,
reservations, identity/access infrastructure, queues, delivery coordinators or
execution mirrors, including inside Fóir records or operations.

Preserve the concrete integration boundaries:

- Client reads use the Fóir SDK with scoped publishable key/current session.
  Use typed nested CMS selections and follow pagination; do not replace these
  with a broader frontend API proxy or mistake a default selection for a limit.
- Operations verify platform dispatch for the expected project/tenant, derive
  identity from ingress, and build data clients from ingress.dispatch. Never
  trust caller-supplied identity or add a general Fóir backend key.
- Provider secrets stay in Fóir under the owner bound to verified dispatch.
  No Worker secret/environment fallback or installation made to bypass a refusal.
- Upload through native uploadFile, PUT bytes and the landing flow. Check record
  and file visibility separately; do not widen private file grants for display.
- Use native limits and server-enforced entitlements for the approved offer.
  Preserve free/paid separation, shared native/web identity and reconciliation.
  Verify required native semantics; do not substitute a custom quota ledger.
- Await bounded work/callback in each dispatch and use native continuations for
  more slices. No second queue or unobserved promise after returning.
- The embedded admin UI uses Fóir's scoped placement session and appearance
  handshake. Keep editable product content/copy/tokens in Fóir, with coherent
  iOS/web defaults. Public placement HTML never grants record access.
- Compose app/website configuration in one root and user pool. Regenerate types
  from actual served scopes after schema/grant changes; never hand-edit them.

When a supported call fails, investigate the served contract, scope and current
known gaps. Fail closed where authority is missing. Record app defects and
unresolved questions on the ticket; do not silently widen permissions or build
replacement infrastructure. Report a dependency that prevents acceptance and
continue independent planned work. Customers consume the maintained platform
inventory; speculative questions and execution journals do not belong in it.

## Deliver and verify

Implement the ticket across its affected iOS, web, console, operations and CMS
surfaces. Preserve live data and unrelated edits. Add replacements, migrate
callers/data, then remove only superseded domain code and its unused grants,
copy, assets, dependencies and tests according to the plan. Retain framework
acceptance tests; update product tests to target the new behavior. Update seed
content, customer docs and agent guidance to describe the resulting product.
Do not turn local cleanup into destructive remote pruning.

Run checks appropriate to the change and the delivery profile. Drive meaningful
success/refusal/retry/account-switch paths, test record/file privacy, build both
clients and verify the embedded console as relevant. Billing acceptance must
prove the approved purchase/restore/reconciliation behavior in its authorized
test environment; fixtures are not live settlement or Apple Sandbox proof.
Record exact source/environment and evidence in the tracker. State any unrun
device, provider, clean-install or deployed checks; do not call the app ready
because compilation passes.

The template must not be published with unfinished advertised functionality.
Prepared code, passing builds, test doubles and disabled switches do not close
feature acceptance. Complete the actual iOS/web/console and provider flows;
for subscriptions prove client purchase/restore through server entitlements.
Report genuine blockers with concrete evidence and affected acceptance, without
misclassifying app/configuration defects. Keep release stopped unless the owner
explicitly decides the blocker's disposition; never silently defer a feature.

Finish each ticket with behavior changed, evidence, remaining dependencies and
next planned work. Deployment, store submission, public publishing, paid calls,
live billing, permission changes and destructive data actions require the scope
and authorization applicable to those actions. Implementing a ticket is not
permission to activate every integration or publish the product.
