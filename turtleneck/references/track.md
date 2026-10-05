# Track in detail

## Statuses

| State | Meaning | Moved by |
| --- | --- | --- |
| Not started | Filed and placed in the sequence | The filer |
| In progress | Claimed and being built | The agent, before branching |
| Landed, awaiting the owner | On the integration branch, proven on the deployed environment, smoke list handed over | The agent, after the deployed smoke |
| Done | In production, and the production check passed | The agent, after the promotion |

The profile maps these to the tracker's own names. If the tracker has no status for the third state, use a label beside its review status. At a hand-over, the only tickets in progress should be ones still being built.

Some trackers close a ticket when a linked pull request merges. That skips the third state, so set the ticket back.

## Comments

Write for a fresh session that has none of your context. Give the commands you ran and the counts they returned. Say what was not done. Read the clock before writing a time. Never paste a secret. Its name and length are enough.

### Start

```
Started <date and time>. Reading <tickets>. Working in <worktree> from <commit>.
```

### Ground truth

```
Measured on <commit>:
- <what exists, with counts>
- <where it differs from the ticket>
Plan: <the pieces, in order>.
```

### Progress, after each proven step

```
<What landed or was proven>, <commit>.
Evidence: <gate result, N of M planted mistakes caught, flows driven>.
Next: <the next step>.
```

### Evidence, after the deployed smoke

```
On <environment> at <version>.
- <flow>: <result>
What I could not show there, and why: <one line each>.
Smoke list for the owner: <the list, or a link to it>.
```

### Stop

```
Stopping <date and time>.
Done: <list>. In flight: <what, where, at which commit>.
To resume: <the exact commands>. Nothing is left running.
```

## Filing

State the fault in the title, in the words of the person who meets it.

Before filing, reproduce the fault, look for a duplicate, and check whether a fix has already landed and is waiting on a promotion. Then place the ticket exactly once.

A leaked credential goes to the owner directly and stays out of the tracker.

At the end of a block of work, list the tickets you filed and the state of each. Anything not fixed needs a reason.

## Decisions

Record each of the owner's decisions on its ticket with the date, in their words where they are short. A recorded decision is a constraint to build to. If you think it is wrong, say so to the owner before you build.

When asked to put back something that was deliberately removed, show the removal and its reason before acting.
