# Shape in detail

Shape work when it spans more than one repository, changes a contract other code depends on, migrates stored data, or will take more than a day or so. For anything smaller, go to Deliver and say on the ticket why it needed no RFC.

## Measuring

Measure on the integration branch at a named commit, and write the commit down. Readers trust an RFC for its measurements, so someone else has to be able to repeat them.

When there are more than three facts, put them in a table: what the thing is, where it is read or written, and the file.

Check a negative before reporting it. Search under several names and in the generated code. A count of zero needs a control that reads non-zero, because a search that never ran also returns zero.

Read the tracker for earlier decisions on the same ground. The RFC has to name the ones it reverses.

Keep two kinds of evidence apart. Design evidence is the schema, the contract and what the code refuses. Migration evidence is what production holds today. To find out which one you are using, state your argument with no production number in it. If nothing is left, what you have is a note for the migration.

## The RFC

Write it in the tracker, as the description of the parent issue or a document linked from it. Put it in the repository only when the build or another document links to it.

```
RFC: <the decision, as a sentence>

Status and date. What raised it. What it depends on.

## The problem
What happens today, measured. A table where there are more than three facts.

## The decision it turns on
The one structural question underneath the request.

## Decision
Numbered. One sentence each, then a paragraph.

## What this amends
Each earlier decision this reverses or narrows, named, with the reason.

## Design

## Rejected alternatives
Each with the reason it lost.

## Not building
What is deliberately left out, and why.

## Open questions
Numbered. Each with a recommendation and the strongest counter-argument.

## Tickets
The phases.

## Complete when
Conditions someone could check: a replay, a diff that reads zero, a flow driven end to end.
```

## Tickets

Write the title as the fault or the missing capability, in the words of the person who meets it. "Staff cannot delete a user" tells a reader more than "Add a delete endpoint".

In the body, give what happens today with its measurement, what should happen, and the acceptance lines. Mark each acceptance line local, deployed or owner for where it will be proven. Add the positive control and what the ticket depends on.

Each ticket sits in exactly one place. Put it at the first point in the sequence after everything it needs, even if its surface belongs to a later phase. A feature split across phases ships half-working.

Name the collision domain. These are the parts of the system the epic owns while it runs, so that nothing else is scheduled into them.

Order the work additive, then migrate, then delete, and never delete something in the landing that creates its replacement.

Sizing is the first deliverable. Estimate from the children and the counts once the ground is measured.

## The hand-over prompt

Post it as a comment on the epic, so the next session finds it with the scope.

```
You are picking up <epic>. Status when written (<date>): <one line>.

What this is: <one paragraph>.

Read first, in this order: <tickets and documents>.
The code is the source of truth and the tickets are the brief. Where they
disagree, measure, then record the disagreement on the epic before acting.

Scope: every item lands and none is deferred.
Settled decisions (constraints, to build to): <list>.

Phases. Each ends with a green integration run and a comment on the epic.
  0. Preconditions, confirmed by measurement. A ticket's status is not proof.
  1. Ground truth, and any tickets still missing.
  2. Additive.
  3. Migrate.
  4. Delete.
  5. Gate, deployed smoke, the owner's smoke list, then hand to the owner
     to time the promotion.

Lessons from earlier work: <what the last piece of work learned>.

Done when: <the condition>.
```

Write settled decisions as constraints. A prompt that says "raise this with the owner before building" about something already decided restarts the argument.

Before handing over, compare the epic's children with the prompt, because scope comments and new tickets accumulate between filings. When the prompt changes, edit the comment in place and say that you did.
