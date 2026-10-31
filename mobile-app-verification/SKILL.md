---
name: mobile-app-verification
description: Build and walk through a native Apple app with MobileBuildMCP, including adaptive and foldable layouts. Use for runtime verification and release evidence, not static code review alone.
---

# Verify the running app

Read the project's AGENTS.md and delivery profile. Preserve the user's working
edits and existing approvals. Establish the exact revision and environment;
never turn a simulator smoke test into a claim about physical hardware.

1. Discover MobileBuildMCP tools and read their current input schemas. Call
   session_show_defaults before the first build/run/test. Discover projects only
   if the context is missing; select a real scheme and installed simulator.
   Prefer build_run_sim for run intent. Use the MCP, not raw xcodebuild/simctl.
2. Build the actual candidate, with its normal configuration and scoped app key.
   Keep signing files, credentials, simulator identifiers and logs outside the
   public repository. A fixture build is separate evidence, not a replacement.
   Inspect build progress before cancelling a cold build: asset compilation can
   take several minutes while still making progress. Preserve useful caches.
3. Capture a fresh semantic UI snapshot before acting. Use current element refs;
   recapture after navigation, rotation or state changes. If interaction tools
   are absent, inspect enabled workflows and enable the supported UI workflow
   locally; do not invent a tool or claim a walkthrough from screenshots alone.
   Confirm the visible Simulator or Device Hub device matches the MCP target.
   A successful tap acknowledgement is not proof that navigation happened. If
   the installed runtime needs a supported computer-use fallback, record that
   distinction and verify the resulting screen after every action.
4. Walk the critical path and a counterexample: fresh/signed-out entry,
   onboarding, primary navigation, detail and media, capture permissions and
   refusal, empty/error/offline/retry, profile/settings, sign-out/account switch.
   For social or paid apps also verify canonical authors, toggle reversal,
   entitlement expiry and purchase restoration using isolated test accounts.
   A test account or sandbox approval is not authorization for live payments.
5. Check compact and expanded windows, large text, light/dark and reduced motion.
   For Duo/foldable requests read the relevant current skills from
   https://github.com/mirzaaghazadeh/iphone-duo-skills and Apple's preparation guide
   https://developer.apple.com/iphone-duo/prepare/ . Verify API availability in
   the installed SDK. Prefer container geometry, independent safe-area edges
   and system containers over device-name branches. Test open/closed/rotation
   and mid-session resizing when tools support it; name missing pose controls.
6. Record build/SDK/runtime, tested screens, observed results, screenshots and
   remaining owner checks. Redact private content before sharing artifacts.
   Fix reproducible defects, rebuild after fixes, and rerun affected flows.
   Physical camera quality, biometrics, push, device-only gestures and store
   purchases remain unverified until tested on appropriate hardware/services.

Use the project's tracker for concrete failures and evidence. Keep the owner's
walkthrough short and limited to checks the automation could not establish.
