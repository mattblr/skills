# Account deletion review

Use Apple's current [account deletion guidance](https://developer.apple.com/help/app-review/guideline-reference/5-1-1-account-deletion)
and [review guidelines](https://developer.apple.com/app-store/review/guidelines/).
Apply the requirements to the actual app; do not infer readiness from a provider
API name or a support link.

- Put an easy-to-find deletion action in account settings. It must initiate
  deletion of the whole account and associated personal/UGC data. Deactivation,
  logout or a support-email request alone is insufficient for an ordinary app.
- Explain permanence and what is removed, retained or still being processed.
  If erasure runs later, distinguish acceptance from completion and verify its
  expected timing and completion notice. Retention claims need actual policy
  facts, not invented legal obligations.
- Support confirmation and recent authentication without making deletion
  unnecessarily difficult. Apple-only and email-code accounts need a supported
  passwordless route. Reauthentication must not automatically submit deletion;
  switching accounts must invalidate the old confirmation.
- Verify the authenticated self-service boundary. A failed/refused request must
  not clear the session or claim deletion. On success, revoke sessions and
  remove local tokens, private caches, push registrations and device notices.
- Exercise in-flight session races: a refresh completing after sign-out or
  deletion must not restore the old session, and its refusal must not clear a
  replacement account. Bind queued credential lookup, response handling and
  cleanup to the initiating session; do not let an earlier mutation acquire a
  newly signed-in account's bearer. Verify late responses cannot repopulate a
  cache shared with the replacement account. After accepted deletion, perform
  local cleanup without depending on another call with the revoked session.
- Trace ownership, not only profile rows: uploaded photo bytes, derived assets,
  notes, private settings and processor copies. Check other users' reposts,
  references and notifications cannot preserve the deleted person's content.
  Do not delete unrelated shared objects or another person's work.
- For Sign in with Apple, verify provider token revocation through Apple's
  supported API and required server notifications. Removing the local identity
  row is not evidence that Apple's authorization was revoked. Check deletion
  followed by fresh registration, not just returning sign-in.
- Explain subscription handling and provide management links before deletion.
  Apple billing may continue after account deletion. Do not require waiting for
  expiry as the only option; verify web-provider cancellation/retention too.
  Never promise that deleting an app account cancels an external subscription.
- Use an explicitly disposable test account. Verify cancel, expired proof,
  network/server refusal, successful closure, eventual record/file erasure,
  old-session refusal and account switching. Do not delete the owner's account
  or real content for a walkthrough. Obtain the applicable authorization for
  the final irreversible test.
- Give reviewers the exact settings path, authentication instructions, erasure
  timing and known limits. Do not call the app review-ready while cleanup,
  Apple revocation or necessary UGC safeguards remain unverified.
