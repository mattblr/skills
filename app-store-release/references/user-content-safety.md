# Verify user-generated content safety

For an app with public posts, photos, comments or profiles, check the current
App Review user-generated-content requirements and exercise the actual flows.
A policy page, cat detector or report button alone does not establish filtering,
report receipt, blocking or an operational response process.

- Separate recognition from safety. A client classifier may suggest what an
  image contains; it cannot authorize server publication or prove that content
  is unobjectionable. Include web uploads and modified clients in the boundary.
- Identify which data becomes shared. Private photo bytes can stay outside
  external screening while names added to a public directory still need their
  own text policy. Disclose the processor and timing accurately.
- Bind approvals to the checked bytes and words. Test changed content, missing
  categories, unsupported input categories, provider errors and failure to save
  a verdict. These must not become successful publication. A refused retry
  must not obtain repeated model votes until one happens to pass.
- Prove reports reach an authorized reviewer and that the reported user cannot
  read the reporter or private details. Cover posts, comments and profiles.
- Exercise block and unblock across canonical authors and reposting accounts,
  including feeds, profiles, galleries, full-screen media, map previews and
  search. Check signed server interactions, account switching and read failures;
  a blocked post must not return as an anonymous photo fallback.
- Distinguish hiding a reported comment from hiding its source image everywhere.
  Verify record access and file bytes separately, existing audience grants,
  paged references and later attempts to repost or widen an audience. Test races
  with publication; do not claim atomic enforcement from a sequential test.
- Warm a successful anonymous/non-owner read before narrowing access, then
  repeat the identical query and unsigned media URL afterward. Capture stale
  and cache headers. A cache-busted or request-bypassed diagnostic does not prove
  that ordinary visitors lose the warmed response. Verify record metadata and
  bytes independently; neither substitutes for the other.
- For resumed work, distinguish accepted dispatch from terminal completion.
  Check that only the initiating user can observe a private run, with refusing
  anonymous, other-user and operator-history controls. Preserve retry identity
  and discard results after account changes.
- Compare full fixture payloads before and after supposed partial/no-op writes.
  A list becoming empty is not privacy evidence if a filter field was erased.
  Check required fields and references, restore isolated fixtures from verified
  snapshots, and avoid blind read/modify/write workarounds for concurrent data.
- Keep moderation decisions attributable and reversible when appropriate.
  Approval of an old checked revision must not approve newer content. A hold's
  release need not republish content automatically. Account suspension, deletion
  and subscription cancellation are separate actions.
- Check generated media too: approval of a source photograph does not approve
  model output. Keep a feature disabled if its output lacks the chosen policy.
- Use isolated synthetic fixtures and the approved provider budget. Do not send
  known or suspected child sexual abuse material to a general moderation API;
  follow the provider's current handling guidance. Never put credentials into
  logs, screenshots, repository files or command arguments.

Record successful and refusing controls, environment/build, operator action,
file-read results and remaining owner checks. Keep unverified provider/device
paths and the response process as release gates. A working app adapter is not
proof that the platform provides the same capability natively.
