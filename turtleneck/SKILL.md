---
name: turtleneck
description: Take work on a large or multi-repo software project through a full delivery lifecycle. Shape it first (measure, write an RFC, get the owner's decisions, file tracked tickets), then deliver each change (build, prove, smoke test in the real browser or app, gate, land, watch the deploy, hand the owner a smoke list, promote), keeping the issue tracker current throughout. Use when planning a feature or epic, writing an RFC, picking up or handing over a ticket, landing or deploying a change, smoke testing, or promoting to production, and whenever the project has a turtleneck.md profile, even if the user only says "ship this" or "pick up the next ticket".
---

# turtleneck

Take work on a large project from an idea to production, with the evidence for each step written down in the issue tracker.

The skill has three parts. Shape turns an idea into tickets worth building. Deliver takes one change from a ticket to production. Track keeps the issue tracker true while both happen. A small fix can start at Deliver. Work that spans repositories, or takes more than a day or so, starts at Shape.

## Read the project's profile first

The steps below say what has to be true. The project's profile says how: its commands, its landing route, its environments, what its statuses mean and what only the owner does. Look for `turtleneck.md` at the repository root, or at the path the project's `AGENTS.md` or `CLAUDE.md` names. In a multi-repo project one repository holds it and the others point to it.

If there is no profile, write one before doing anything else. Read the CI workflows, branch rules, deploy configuration and tracker, fill in [the profile template](references/profile.md), and ask the owner only for what the repository cannot tell you. Where the profile and this file differ, follow the profile. Some rules here depend on a project's conditions, and the profile is where those conditions are stated.

## Shape: before an epic exists

Do not start building until the tickets exist. A large change that goes straight to code skips the decision record and the breakdown the owner needs to see.

1. Read the intent. Read the tracker for what was asked and what has been decided before you read the code. Code shows what exists and says nothing about what was meant, so do not read "not built" as "not wanted".
2. Measure the ground. Find and count what the change touches on the current integration branch, and record the commit you measured. A file and line cited in an older ticket was true on the day it was written, so check it again.
3. Find the decision it turns on. Most features hide one structural question. State the target design and argue for it from the design. Use today's row counts and usage to size a migration, and keep them out of the argument for the design.
4. Write the RFC in the tracker. Give the problem with its measurements, the decision, the earlier decisions it reverses, the design, the alternatives you rejected and why, what you are deliberately leaving out, and what will be true when the work is complete.
5. Put the open decisions to the owner. Keep them few and in plain English, each with a recommendation and its strongest counter-argument. Record each answer with its date. Anything that widens who may do something gets a question of its own, because a general "agreed" does not cover it.
6. Break it down. File one ticket per piece that can land on its own. Each ticket carries its acceptance, a control that proves its check can fail, and where it will be proven: locally, on the deployed environment, or by the owner. Place every ticket exactly once. Order the work additive, then migrate, then delete, so that each landing leaves the main branch in a state it can live in.
7. Hand over. Post a self-contained prompt on the epic. It names what to read first, the settled decisions as constraints, the phases, the lessons from earlier work and the condition that ends it.

[Shape in detail](references/shape.md) has layouts for the RFC, the tickets and the hand-over prompt.

## Deliver: one change, from ticket to production

Each step ends with a condition. Meet it before starting the next step, and say so when you cannot.

1. Pick up. Read the ticket, its children and its newest comments. Claim it in the tracker before creating a branch. Work in a fresh worktree off the integration branch, and post what you measured before changing anything. Done when a start comment and a ground-truth comment are on the ticket.
2. Build. Build the whole scope locally as commits, in the profile's dependency order, and regenerate derived code at each step. Done when every module you touched builds.
3. Prove. Give each test a positive control, because a check that finds nothing has to show that it looked. Then plant mistakes in the code your important tests protect and count how many are caught. Done when you can report N of M caught, with each survivor explained.
4. Local smoke. Start the built artifact locally and drive the product as a user would, in the browser or in the app itself. Walk the paths that should succeed as well as the ones that should refuse. Done when you have seen each changed flow work and named anything you did not drive.
5. Gate. Run the profile's full local mirror of CI once, on the exact tree that will land, and leave that tree alone while it runs. Done when it is green and you have named the CI jobs the mirror cannot run.
6. Land. Make one landing per repository for the whole piece of work, by the route the profile gives. Done when the integration branch holds your change.
7. Watch. The integration run starts when you land, so the change is not landed until you have read that run. Watch it in the background with a deadline, read every job, and confirm the deployed environment reports the version you landed. Done when every run is green and the version matches.
8. Deployed smoke. Drive the same flows on the deployed environment, to cover what only it has, such as real third parties and the real edge. Done when an evidence comment is posted and the ticket is in its "landed, awaiting the owner" status.
9. Owner smoke. Hand the owner a short numbered list of the flows worth a person's eye and every step you could not take yourself, with the test objects left ready. Done when the owner confirms, or reports what broke.
10. Promote. Once the owner has smoked the change or waived that, promote the way the profile says. The owner makes the production push. Check that production serves the new version, then close the tickets. Done when the tickets are closed with their evidence.

A fault found at any step sends the work back to Build, and every later step runs again on the new tree. Local smoke sits before the gate for that reason: the gate is the slowest step and its result only holds for the tree it ran on.

If you have no way to drive a browser or the app, say so once and move every flow in steps 4 and 8 onto the owner's list. Reading the code for a flow does not count as seeing it work.

[Deliver in detail](references/deliver.md) covers positive controls, planted mistakes, what a smoke record holds and the owner's list.

## Track: keep the tracker true

Sessions end and their context goes with them. The tracker is the one record that every agent and the owner can read, so write to it as you go, for a reader who has none of your context.

Claim a ticket by moving it to its in-progress status before you branch. Other sessions cannot see a local branch, so the status is the claim.

Comment after every proven step. Say what was proven, with the commands and counts, and what comes next. When you stop, say what is in flight and how to resume it.

Keep one meaning per status. A ticket that is being built, one that has landed and is waiting for the owner, and one that is done after production are in three different states. Use the profile's names for them, and never close a ticket on a green build alone.

Let one person file. Whoever coordinates the work files new tickets and places each exactly once, and everyone else reports to them. That keeps duplicates out.

Fix what you file. A defect you find and file is yours to fix in the same block of work, unless the fix needs a decision from the owner. Say which it is.

Put decisions in the tracker and invariants in the code. Analysis and reasoning date quickly and belong on tickets. A rule that a future change must not break belongs in a comment where it is enforced.

[Track in detail](references/track.md) has the comment layouts and a status table.

## What belongs to the owner

Some actions stay with a person: the production push, rotating secrets, typing credentials into a host that is not local, permanent deletion, and any decision that widens access. The profile lists them for this project. When you reach one, say so in a sentence, hand over the exact command or click list, and carry on with everything that does not depend on it.

[Why each step is there](references/why.md) gives the failure behind each step and says which rules depend on a project's conditions.
