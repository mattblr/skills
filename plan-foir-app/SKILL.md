---
name: plan-foir-app
description: Turn a discovered app brief into a refactor plan for an existing Fóir template, identifying what stays or changes and creating workstreams with dependency-ordered implementation tickets. Use after product discovery, before building.
---

# Plan the app refactor

Consume the product brief and settled decisions from discovery. Read AGENTS.md,
README, the documentation guide and delivery profile. If the brief is missing,
return to the template's discovery skill; ask only consequential unanswered
questions, not the whole interview again. This skill analyzes and files the work;
build-foir-app implements it.

## Preserve the foundation

The template demonstrates an iOS app, web app/website, subscription purchases
and server-enforced entitlements, plus an admin console embedded in Fóir.
Preserve that integrated framework and its managed-backend feature coverage.
Keep shared identity, native/web billing, scoped SDK reads, verified operations,
native uploads, notifications/execution, CMS/copy/design tokens, generated clients
and build/deployment tooling. Adapt their product rules and configuration.
An unrelated app idea is not authorization to delete the framework. A free
launch retains subscription plumbing with paid experiences inactive. Record any
explicitly requested framework reduction as a scope decision, not an inference.

## Compare the brief with the implementation

1. Read current tracker decisions before measuring source. Record the revision
   and relevant uncommitted state. Inventory concrete models/relations, grants,
   operations/hooks/schedules, iOS/web screens, embedded console controls,
   CMS/copy/tokens/seed/assets, subscription products/benefits, generated clients
   and checks. Treat generated types as derived contracts, not business logic.
2. Discover current Fóir MCP tools/schemas through OAuth and select the user's
   workspace/project/environment and organization where applicable. Inspect
   supported native capabilities before proposing backend work. Read the served
   no-backend and app-architecture guides and the template's confirmed gaps.
   Read-only planning does not authorize remote writes. Do not infer deployed
   capability solely from local platform source or a client's default selection.
3. Produce a change matrix. For each affected area give its actual source path,
   current behavior, target behavior, keep/adapt/add/remove decision, reason and
   dependencies. Mark shared framework pieces as keep or adapt explicitly.
   Restrict removal to superseded application-specific artifacts and their dead
   callers. Separate local source cleanup from installed-data migrations.
4. Map the domain and workflows to Fóir-native models, ownership/access, files,
   limits/entitlements, notifications and operation execution. Only application-
   specific logic belongs in handlers. Never plan app-owned identity, access,
   metering/ledger/reservation infrastructure, a second queue, broader credential
   proxy or provider-key environment fallback, even inside Fóir records.
5. Reconcile the brief with supported behavior. Confirm substantive new product
   tradeoffs; record unsupported assumptions as questions in the tracker. Do not
   mislabel unfinished app integration as a platform gap or ask customers to
   implement platform replacements. Preserve previously settled answers.

## Workstreams and tickets

Use the bundled turtleneck Shape workflow and the project's tracker conventions.
Select the customer's tracker/team/project explicitly; do not inherit a template
maintainer's issue destination. Inspect existing work to avoid duplicate epics or
tickets. If no tracker is connected, prepare the concrete plan/ticket bodies and
request the missing destination; do not claim tickets were created.

Write the brief, change matrix and target design on an epic/RFC. Group tickets
into workstreams with clear ownership/collision areas, dependencies and useful
parallel boundaries. Cover domain/schema/access/operations, iOS, web, console,
commercial configuration, CMS/copy/design and verification where affected.
Start with a real end-to-end slice, then expand. Keep each ticket independently
reviewable; sequence additions, caller/data migration, then obsolete code removal.
Do not remove the old path in the same landing that introduces its replacement.

Each ticket must state the user-visible outcome; current/target behavior;
concrete affected paths and contracts; foundation to preserve; implementation
scope; dependencies; measurable acceptance with meaningful success/refusal
controls; and where evidence must be collected (local, deployed or device/owner).
Include schema/grant regeneration, existing-data compatibility, rollback and
release actions when relevant. Do not hide device/provider acceptance inside a
local-test checkbox or make a ticket for every file.

Finish with linked workstreams/tickets, dependency order, first ticket to build,
open decisions, acceptance boundary and a self-contained handoff to build-foir-app.
Keep plans, status and evidence in the tracker, not customer documentation. Do
not refactor source, apply schema/grants, activate billing, deploy or publish as
part of planning. Ticket creation is the output, not proof the app is built.
