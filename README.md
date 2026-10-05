# Skills by Matt Blair

Skills for the things I build. Each folder contains a `SKILL.md` your coding agent can read.

## avatar-me

You've probably seen apps with those fun little avatars for each user. [avatar-me](avatar-me) helps you make your own, using the logo and colours already in your codebase.

![Ormitar's hidden companions peek out and form a grid.](avatar-me/media/ormitar.gif)

The skill grew out of building Ormitar for [Fóir](https://foir.io), with [Blobatar by Alain00](https://github.com/Alain00/blobatar) as the original inspiration. It guides the agent through finding a character, choosing a signature gesture, and building an independent component in your project.

[See the design process and installation instructions](avatar-me/README.md), or [read about it on mattblr.com](https://mattblr.com/skills/avatar-me).

## turtleneck

[turtleneck](turtleneck) gives your coding agent a process for work on a big project, from the first analysis through to production. The agent writes an RFC before any ticket is filed. For each change it drives the real app as a smoke test, then hands you a short list of what to check yourself.

It comes from work on large enterprise software projects. Your project's commands go in a `turtleneck.md` profile, which the skill writes on its first run.

[See the steps and installation instructions](turtleneck/README.md).

## Install a skill

Clone this repository and copy the folder for the skill you want into your agent's skills directory. For Codex:

```sh
git clone https://github.com/mattblr/skills.git
mkdir -p ~/.codex/skills
cp -R skills/avatar-me ~/.codex/skills/avatar-me
```

For Claude Code, install it for your user:

```sh
mkdir -p ~/.claude/skills
cp -R skills/avatar-me ~/.claude/skills/avatar-me
```

Or copy `avatar-me` into `.claude/skills/avatar-me` inside a project to share it with that project's contributors. In Claude Code, invoke it with `/avatar-me`, followed by what you want to build. For example:

> /avatar-me Make a character from our logo, with a few variations for user profiles. Show me the resting pose and a signature animation first.


Skill instructions are MIT licensed. The Fóir and Ormitar artwork illustrates the case study and remains brand material; see [LICENSE](LICENSE).
