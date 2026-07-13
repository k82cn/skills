# k82cn Skills

Personal Codex skills maintained by k82cn.

This repository is intended to collect reusable skills, workflows, scripts, and
reference material that extend Codex for recurring tasks.

## Repository Layout

Each skill should live in its own directory and include a `SKILL.md` file:

```text
skill-name/
  SKILL.md
  agents/
    openai.yaml
  scripts/
  references/
  assets/
```

- `SKILL.md` describes when the skill should be used and the workflow Codex
  should follow.
- `agents/openai.yaml` contains recommended UI metadata and a default prompt.
- `scripts/` contains helper scripts used by the skill.
- `references/` contains supporting documentation or examples.
- `assets/` contains reusable templates, images, or other static files.

Only `SKILL.md` is required. Add the other directories when they make the skill
clearer or easier to reuse.

## Available Skills

- [`code-review`](code-review/SKILL.md): Reviews designs and implementations for
  behavioral, security, compatibility, concurrency, testing, documentation, and
  maintainability risks. It routes feature, fix, and refactor reviews to focused
  guidance and remediates authorized findings within ownership boundaries.

## Authoring Guidelines

- Keep each skill focused on a specific workflow or domain.
- Prefer concrete steps and local scripts over long prose instructions.
- Include examples when they clarify expected inputs or outputs.
- Avoid storing secrets, tokens, or private environment-specific data.

## Installation

Clone this repository into your Codex skills directory:

```sh
git clone git@github.com:k82cn/skills.git "$CODEX_HOME/skills/k82cn"
```

If `CODEX_HOME` is not set, Codex commonly uses `~/.codex`:

```sh
git clone git@github.com:k82cn/skills.git ~/.codex/skills/k82cn
```

## License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE).
