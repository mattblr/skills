# Why each step is there

These steps come from work on large enterprise software projects. Each one answers a failure that happened without it. The last section lists the rules that only hold under certain conditions.

## The failure behind each step

Local smoke came from a command-line bundle that passed 825 tests and could not start. The tests imported the source and never loaded the bundle. On another occasion, running the real console against a local stack found two faults that every gate had passed.

Positive controls came from a filtered test run in a local gate. It named the wrong package, matched no tests, and had been reporting green on an empty set.

On one fix, the first round of planted mistakes caught 5 of 11. The tests checked that nothing was let through and never checked what a caller was handed back, so they were fixed before the gate ran.

Watch exists because a change was reported landed once its deployed smoke passed. The integration run behind it stayed red for ten hours, on three guard jobs that a smoke test could not have shown.

Deployed smoke stayed in the loop after a sweep of 137 green packages was followed by a deployed smoke that found two defects. One was in the only path real callers used.

The rule of one landing per repository followed a feature that went out as eight pull requests, four of them stacked. The runs queued behind each other, and the contention produced failures that looked like faults in the code.

Shape came from a build that its owner stopped part way, asking for the RFC and the tickets first. As code alone, the work could not be tracked or reviewed as a plan.

Two agents once started the same ticket, which is why a claim is made by status. The first had made a branch and left the ticket's status alone.

## Rules that depend on a project's conditions

Check that your project shares the condition before adopting any of these.

Landing without a pull request per change fits a project with long CI runs, no preview environments and no second reviewer. There, changes are merged locally and pushed to the integration branch, and that branch's run is the only CI. A pull request would add a wait and show nothing a local run had not.

Working in series fits a project where parallel agent sessions are costly. The owner is asked before any are started.

The owner times every promotion when live customers depend on production.

On a deployed host, the agent smokes through a session the owner has signed in to. Creating accounts, typing passwords and permanent deletion stay with the owner.
