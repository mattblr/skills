# Deliver in detail

One section per step. The project's profile supplies the commands.

## Pick up

Read the comments newer than the ticket's description and newer than any hand-over. Scope accumulates in comments, and another session may already have picked the hand-over up. Check for an existing branch or worktree as well as the ticket's status.

Work in a fresh worktree off the integration branch. A shared checkout may hold another session's uncommitted work, so never stash, reset or clean one.

The ground-truth comment says what you measured, on which commit, and where it differs from the ticket. Reproduce a defect through the real path before fixing it.

## Build

Build the whole scope before landing any of it. A commit costs nothing and a landing costs a CI run.

Follow the profile's dependency order, and regenerate derived code where the project generates it. Hand edits to generated files are lost at the next regeneration.

Build the correct solution now. Nobody schedules the change that would replace a stopgap.

Stage files by explicit path, so that a broad add cannot sweep in work that belongs to someone else.

## Prove

### Positive controls

A test filter that matches no tests exits green. A scan that returns zero may never have run. Pair every check with something that must be non-zero: the test names in the output, a count of what was scanned, or a known value the search has to find.

### Planted mistakes

Tests are evidence only if they can fail for the reason you care about. Planting mistakes shows whether they can.

1. Commit first, so that restoring is exact.
2. Choose the lines your important tests exist to protect. Change each the way a real mistake would: flip a comparison, drop a condition, return early, widen a permission.
3. Run the tests that claim to cover the line. The mistake is caught when a test fails for the right reason.
4. For a threshold, change it at the boundary as well as at the extremes.
5. Work out why each survivor survived. The test may be missing, in which case write it. The change may make no observable difference, in which case say why. Or the probe may never have reached the code. To rule that out, plant something that cannot compile in the same place.
6. Restore each file from a copy. Reverting the whole working tree destroys uncommitted work that was never yours.
7. Report N of M, with each survivor explained.

## Local smoke

Build what ships, whether that is a bundle or a binary, and run that. Tests usually import the source, so a bundle that cannot start still passes them.

Start it with an explicit environment, on a database built from your branch's migrations. A service that inherits the shell's settings can point at a different database from the service beside it, and nothing will report an error.

Drive each changed flow as a user would. Take the path that should succeed first, then the ones that should refuse, and read what an error looks like to the person who receives it.

Keep a smoke record of each flow, the account or role you used, what you saw, and what you did not drive and why.

Stop the local servers by process id before any gate that reads the same tree.

## Gate

Read the CI workflow to see what the gate has to mirror. A step missing from the mirror has not passed, so name it.

Run the whole workspace uncached. Guards usually live above the packages, and a run of the package you edited will not reach them.

If the integration branch moved since you branched, the rebased tree is a new tree and needs its own gate.

A failure reported part way through is not the end of the run. Let the run finish, or stop it, before you edit anything.

A failure blamed on the environment needs evidence. Run the same check on an untouched checkout first.

## Land

Land in dependency order, one landing per repository. A change that widens a contract ships the provider first, and a change that narrows one ships the consumers first. Where the pipeline can merge queued builds into one, wait for each deploy before the next landing.

Use the route the profile gives. A pull request per change earns its wait when a reviewer or a preview environment is there to use it. Without either, it adds a CI run and nothing else.

## Watch

Start a background watcher with a deadline and work on something else. Do not wait in a foreground loop, and do not leave a poll running against production.

Read the list of jobs as well as the summary line. Some guards run only on the integration branch, and a smoke test cannot see them.

Ask the running service which version it serves. The value stored in configuration can differ from what is running.

## Deployed smoke

Cover what only the deployed environment has. Everything else was proven locally.

On a shared environment, read freely and make only reversible writes, on throwaway objects named so that anyone can tell they are safe to delete.

The evidence comment holds the version, each flow with its result, and what is left for the owner.

## Owner smoke

Keep the list to a few minutes of work, and write each step so that it can be followed cold.

```
Smoke list for <ticket>, on <environment> at <version>

1. Sign in as <role>. Open <page>. You should see <result>.
2. <action>. You should see <result>.

Not done by the agent, and why: <one line each>.
Left ready for you: <the named test objects>.
```

Put on it anything that needs a person's judgement, such as how a screen reads, and every step from the profile's owner list.

## Promote

Promote the integration branch as one merge per repository. Everything in it has already been proven, so the promotion only has to move it.

A migration that removes something gets its own deploy, after the code that stopped using it is live everywhere.

Hand the owner the exact command for the production push. Afterwards, confirm the version production serves, send one real request down each path that differs in production, then move the tickets to done.
