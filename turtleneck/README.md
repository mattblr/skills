# turtleneck

turtleneck gives your coding agent a process for work on a big project, from the first analysis through to production. It suits projects with several repositories or more than one agent working at once, where a change can pass its tests and still be broken when someone opens the app.

<img src="media/turtleneck.svg" alt="A sketch of a black turtleneck jumper with no head and one fist raised." width="260">

## What it does

The skill has three parts.

Shape runs before any ticket is filed. The agent reads what was asked, measures what exists, writes an RFC in your tracker and puts the open decisions to you. Tickets come after your answers.

Deliver takes one change from its ticket to production:

1. Pick up the ticket and post what was measured.
2. Build the whole scope locally.
3. Prove it, by planting mistakes and counting how many the tests catch.
4. Smoke test locally, driving the real browser or app.
5. Gate it on a full local mirror of CI.
6. Land once per repository.
7. Watch the integration run and confirm the deployed version.
8. Smoke test again on the deployed environment.
9. Hand you a short list of what to check yourself.
10. Promote, with you making the production push.

Track keeps the tracker current while that happens. The agent claims a ticket before it branches and comments with its evidence after each proven step, so a fresh session can carry on from the ticket alone.

## The smoke tests

Steps 4, 8 and 9 are the review. The agent drives the real product twice, once on a local stack before anything lands and once on the deployed environment afterwards. Then it gives you a numbered list of the flows to repeat, along with anything it could not do itself, such as signing in as a second user. The list is meant to take you a few minutes.

## Use it

Clone the skills repository, then copy the `turtleneck` folder into your agent's skills directory. For Codex:

```sh
git clone https://github.com/mattblr/skills.git
mkdir -p ~/.codex/skills
cp -R skills/turtleneck ~/.codex/skills/turtleneck
```

For Claude Code, install it for your user:

```sh
mkdir -p ~/.claude/skills
cp -R skills/turtleneck ~/.claude/skills/turtleneck
```

Or copy `turtleneck` into `.claude/skills/turtleneck` inside a project to share it with that project's contributors. In Claude Code, invoke it with `/turtleneck`, followed by the work. For example:

> /turtleneck Customers want to export their data. Measure what exists, write the RFC and put the open decisions to me before filing anything.

In Codex, ask:

> Use $turtleneck to pick up the next ticket and take it through to my smoke list.

The skill works with agents that read `SKILL.md`. It has no runtime package to install.

## Your project's profile

The skill describes what has to be true at each step. How your project does it goes in a `turtleneck.md` file in your repository: the gate command, the landing route, the environments, your tracker's status names and the things only you do.

On its first run the agent writes that file from your CI workflows, branch rules and deploy configuration, asks you for what it could not find, and shows you the result. [The profile template](references/profile.md) lists what it holds.

Some rules depend on your project. A team with reviewers and preview environments should land by pull request. A solo project with slow CI might push straight to its integration branch. The profile is where you say which you are.

## Where it came from

The steps come from work on large enterprise software projects, the kind with several repositories and one person deciding when anything reaches production. Most of them exist because something went wrong without them. A command-line bundle once passed 825 tests and could not start. A change was reported landed while the run behind it stayed red for ten hours.

[Why each step is there](references/why.md) has the rest, and says which rules depend on a project's conditions.

The skill instructions are available under the [MIT licence](LICENSE).
