# Skills

This repository can carry reusable **Codex skills** alongside shared modes/standards/tools.

## Available skills

- [`ado-workitem-dossier`](./skills/ado-workitem-dossier/SKILL.md) — Export an Azure DevOps work item (+ parent + children) into a single Markdown dossier file in `WorkItems/<id>-<title>.md`.

## How to use

- Reference the skill file directly when prompting Codex, for example:
  - `[$ado-workitem-dossier](./skills/ado-workitem-dossier/SKILL.md) Export work item 12345 into a dossier markdown file.`

