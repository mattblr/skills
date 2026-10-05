# The project profile

The profile is one file, `turtleneck.md`, kept in the project. It turns the steps in `SKILL.md` into this project's commands and rules. It holds no secrets and no status. What is in flight belongs in the tracker.

## Writing one

Read the project before you ask the owner anything. Most of the profile is already written down somewhere:

- the CI workflow files, for what the gate has to mirror and how long a run takes;
- the branch rules, for the integration branch, the production branch and who may push to each;
- the deploy configuration, for the environments and how each reports its version;
- the build files, for the build, test and code generation commands;
- the tracker, for the status names in use.

Ask the owner only for what the project cannot tell you: what stays with them, what the statuses mean to them, and which accounts and data are safe to test with. Then show them the finished profile before relying on it.

Record the conditions as they are, because several rules depend on them. A project with fast CI, reviewers and preview environments should land by pull request. A project with none of those gains nothing from one.

## A blank profile

```markdown
# turtleneck profile: <project>

## Repositories
<name>: <what it holds>. Integration branch <branch>, production branch <branch>.
Landing order: <first> then <next> then <last>, and why.

## Conditions
- CI run time: <minutes>
- Preview environments: <yes or no>
- Reviewers other than the owner: <yes or no>
- Agents working at once: <number, and the rule for more>

## Landing route
<Direct push or pull request, per repository, and who may bypass what.>

## Commands
- Build: <command per repository>
- Regenerate derived code: <commands, and which step needs them>
- Test database or fixtures: <how to build one from a branch>
- Local stack: <how to start the built artifact with an explicit environment>
- Gate: <the full local mirror of CI, and the CI jobs it cannot run>
- Watch a run: <command>
- Deployed version: <how each environment reports it>

## Environments
- Local: <ports, databases, what must never be touched>
- Deployed: <hosts, what data it holds, what is safe to write>
- Production: <hosts, how it is read, by whom>

## Smoke
- Driving the product: <browser tool, built CLI, simulator>
- Test accounts and the workspace to use: <names>
- What a local run cannot show: <list>

## Tracker
- Where: <tracker and project>
- Status names: in progress = <name>, landed and awaiting the owner = <name or label>, done = <name>
- Who files: <role>

## The owner's list
<What only the owner does: production pushes, secrets, credentials on a
non-local host, permanent deletion, access-widening decisions, and anything
else particular to this project.>

## Traps
<Short notes on what has gone wrong here before, each with its symptom.>
```
