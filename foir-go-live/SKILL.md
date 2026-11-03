---
name: foir-go-live
description: Prepare and verify a Fóir app's dev-to-production cutover, including published-only hosting, drafts preview, identity, operations and rollback. Use for environment promotion and go-live checklists.
---

# Promote the app safely

Read AGENTS.md, the root config, delivery profile and newest tracker decisions.
Record source/target environments and user authorization. Confirm OAuth standing
and explicit workspace/project/organization before writes. Read served schemas;
never derive production identifiers from dev credentials or browser storage.

Preserve the template's iOS/web/subscription/embedded-console foundation and
Fóir integrations. Promote the planned application-specific refactor, with only
superseded domain code removed. Distinguish local cleanup from authorized
migration of installed data. Do not discard framework support to pass a gate.

Fóir is the managed backend. Promote app-specific logic and supported managed
configuration; do not add app-owned metering, financial ledgers, reservation
services, queues, identity or access-control infrastructure in operations or
records to close a release gate. When starting from a template, consume its
maintained known-gaps inventory and distinguish platform limitations from
unverified integration. Maintaining that inventory belongs to development of
the template itself, not to customers setting up or developing their own app.
The inventory contains confirmed platform limitations only. Put unresolved
questions, release gates and verification evidence in the issue tracker, not
in customer setup documentation.
Discover the current [no-backend](https://docs.foir.dev/no-backend) and
[app architecture](https://docs.foir.dev/guides/app-architecture) guides through
Fóir's served documentation tools when choosing the integration contract.
Local platform source alone does not establish deployed behavior.

Make a concrete add → migrate → remove checklist before cutover:

1. Inventory models, grants, generated clients, locales/design tokens, CMS
   records/files, installations and credentials, operation/manifest/placement
   URLs, auth providers/clients/return origins, first-party login DNS, upload/CDN
   origins, inbound webhooks, purchases and native build configuration.
2. Decide fresh production versus data migration. Keep dev identities, private
   records and media out of a fresh production app. Export reviewed CMS content
   with references/translations and files deliberately; do not treat a fallback
   seed that skips existing records as a complete content migration.
3. Apply the one root configuration to the explicitly selected production scope
   without force/prune or broad release of unrelated pending definitions.
   Review exact grant changes. Create only required scoped keys, keep them
   private and regenerate clients from each served surface.
4. Separate the published site key from a CMS-only drafts key. Keep draft keys
   server-only. Resolve preview audience explicitly; an unguessable URL or
   noindex is not authentication. Respect the user's selected access method;
   do not add a provider-specific gate they rejected. Check draft references,
   media visibility, caching and exclusion of app/user/operation surfaces.
   Verify project-user identifiers from the selected project roster; do not
   assume a console account ID is the hosted project account. Use verified
   immutable subjects for allowlists, never an email or request header.
5. Build reproducibly with private environment inputs. Confirm published-only
   positive/negative controls, draft preview access/refusal, signed-out privacy,
   hosted login/refresh/logout/account linking, upload landing, signed dispatch,
   console handshake and provider webhook completion. A local fixture does not
   prove production configuration. Keep paid features off unless authorized.
6. Deploy additive replacement hosts first. Verify DNS/TLS, exact deployed
   version, canonical URLs, robots/sitemap, redirects, headers and asset/CDN
   access. Migrate all dependants, including native clients and installed
   operation endpoints, before removing the old hostname. Keep rollback routing
   and credentials available; do not delete data or reinstall to move a host.
7. Retire the obsolete route only after dependency checks pass. Verify it is
   gone or follows the agreed redirect, and recheck auth, operation execution
   and webhook state on replacement hosts. Record evidence in the tracker.

Do not promote or publish a template with unfinished advertised features.
Complete their end-to-end acceptance first; disabling a switch, moving work to
the tracker or listing a known gap is not completion. If an external dependency
blocks acceptance, report its exact evidence and impact and keep release stopped
until the owner explicitly decides its disposition. Separate missing app setup
from a verified platform blocker. Do not invent a reduced product scope to ship.

The release artifact should list completed checks, remaining gates, owner-only
facts/actions and rollback commands/configuration. Do not declare live based on
a successful build or HTTP 200 alone. Do not push, release stores, enable live
payments, rotate credentials or widen access outside the user's authorization.

Primary reference: https://docs.foir.dev/ai/mcp . Retrieve current CLI/MCP and
provider documentation for the selected environment rather than assuming that
a dev-only command or continuation contract exists unchanged in production.
