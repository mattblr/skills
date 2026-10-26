# rust

rust gives your coding agent house rules for Rust: how to write it, test it and review it. The compiler and clippy check a lot. These rules cover the judgement calls they can't check, such as whether an error is the right kind, whether output comes out in the same order on every run, and whether a test could ever fail.

## What it does

The agent loads the skill whenever it writes, changes, reviews or ports Rust, or touches a crate's `Cargo.toml`, lints, error types, tests or CI. It then works to nine groups of rules, each with the reason behind it:

1. **Lints are the floor.** One lint config for the workspace, narrow `#[expect]` overrides that give a reason, and restructuring along a real seam when a size limit fires.
2. **Panics and errors.** The failure mode follows the cause, library errors are typed, boundaries decode strictly, and recursion over input has a depth limit.
3. **Determinism.** Anything that reaches output has a defined order, and the outside world is passed in so tests control it.
4. **The compiler carries the rule.** Enums instead of flags, no `bool` in a public signature, and exhaustive matches on your own enums.
5. **Porting from another language.** Keep the domain and drop the old language's habits, with any byte-for-byte compatibility kept in one place.
6. **Tests that can fail.** Write the failing test first, break the code to prove a test catches it, count what actually ran, and test the artifact users install.
7. **Async.** No lock guard held across an `.await`, and public types that are `Send` and `Sync`, checked at compile time.
8. **Dependencies, features and `unsafe`.** Dependencies declared once, additive features, and no `unsafe`.
9. **Docs, comments and logs.** Canonical doc sections, comments that give the reason rather than the history, and structured logs.

It ends with a checklist the agent runs before it says it's done, and a way to review: cite the rule or guideline for each finding, and rank findings by consequence.

## Built on Microsoft's guidelines

The rules build on Microsoft's [Pragmatic Rust Guidelines](https://microsoft.github.io/rust-guidelines/). [references/guidelines.md](references/guidelines.md) links all 90 by area, pinned to the commit the rules were checked against, so the agent reads only the ones that apply. Your repository's own `CLAUDE.md` or `AGENTS.md` comes first, these rules second and the guidelines third.

## Use it

Clone the skills repository, then copy the `rust` folder into your agent's skills directory. For Codex:

```sh
git clone https://github.com/mattblr/skills.git
mkdir -p ~/.codex/skills
cp -R skills/rust ~/.codex/skills/rust
```

For Claude Code, install it for your user:

```sh
mkdir -p ~/.claude/skills
cp -R skills/rust ~/.claude/skills/rust
```

Or copy `rust` into `.claude/skills/rust` inside a project to share it with that project's contributors. Claude Code loads it on its own when it works on Rust, and you can invoke it with `/rust`, followed by the work. For example:

> /rust Port this module from Go, then show me that each new test fails when the code it guards is broken.

In Codex, ask:

> Use $rust to review this crate's error handling, citing the rule behind each finding.

The skill works with agents that read `SKILL.md`. It has no runtime package to install.

## Where it came from

The rules come from porting a compiler and its runtime from Go to Rust with coding agents, with every output checked byte for byte against the original. They describe what kept that work correct.

The skill instructions are available under the [MIT licence](LICENSE). Microsoft's guidelines are linked, not copied, and keep their own MIT licence.
