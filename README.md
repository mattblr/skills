# Skills by Matt Blair

Skills for the things I build. Each folder contains a `SKILL.md` your coding agent can read.

## avatar-me

You've probably seen apps with those fun little avatars for each user. [avatar-me](avatar-me) helps you make your own, using the logo and colours already in your codebase.

![Ormitar's hidden companions peek out and form a grid.](avatar-me/media/ormitar.gif)

The skill grew out of building Ormitar for [Fóir](https://foir.io), with [Blobatar by Alain00](https://github.com/Alain00/blobatar) as the original inspiration. It guides the agent through finding a character, choosing a signature gesture, and building an independent component in your project.

[See the design process and installation instructions](avatar-me/README.md), or [read about it on mattblr.com](https://mattblr.com/skills/avatar-me).

## Install a skill

Clone this repository and copy the folder for the skill you want into your agent's skills directory. For Codex:

```sh
git clone https://github.com/mattblr/skills.git
mkdir -p ~/.codex/skills
cp -R skills/avatar-me ~/.codex/skills/avatar-me
```

Skill instructions are MIT licensed. The Fóir and Ormitar artwork illustrates the case study and remains brand material; see [LICENSE](LICENSE).
