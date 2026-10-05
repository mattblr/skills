# Working on this skills repository

Each skill lives in its own folder at the repository root. Start by reading that folder's `SKILL.md`; its YAML `name` matches the folder name. `avatar-me` is the first skill.

When adding a skill, give it a clear description of when it applies. Keep the main instructions focused, and put longer examples in linked `references/` files when they help. Add an entry to the root README and include installation and invocation examples for both Claude Code and Codex.

Claude Code discovers personal skills in `~/.claude/skills/<name>/SKILL.md` and project skills in `.claude/skills/<name>/SKILL.md`. Invoke a skill as `/<name>`. Codex uses `~/.codex/skills/<name>/SKILL.md` and `$<name>`. The `agents/openai.yaml` file is optional Codex metadata; Claude Code reads `SKILL.md`.

For avatar-me, preserve the requirement for an independent component in the target project's stack. The Ormitar media documents the example that informed the skill. Do not turn it into a required visual style or add a dependency on Ormitar or Blobatar. Keep the signature animation suggestions original; do not add Ormitar's roll.

Use ordinary, specific language in documentation. Describe what a skill does and what the reader should do next. Keep inspiration credits and distinguish reconstructed design studies from recordings. Check local links, frontmatter, referenced files, and any runnable examples before committing. New media needs descriptive alt text and a still alternative when used on a website.

The repository's MIT licence covers the skill instructions. The Fóir and Ormitar brand artwork is excluded, as explained in LICENSE. Do not commit credentials, private project configuration, or source copied from an unrelated repository.
