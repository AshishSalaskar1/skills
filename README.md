# Agent Skills

[![skills.sh](https://skills.sh/b/AshishSalaskar1/skills)](https://skills.sh/AshishSalaskar1/skills)

A collection of reusable skills that give AI coding agents focused workflows and capabilities. Each skill is self-contained under [`skills/`](skills/) with its agent instructions, references, scripts, and supporting assets.

## Skills

| Skill | Overview | Details |
|---|---|---|
| [Memory Hub](skills/memory-hub/) | Durable, repository-local memory for decisions, directions, unfinished work, capabilities, and feedback. Supports focused retrieval, Markdown exports, and an optional local browser. | [README](skills/memory-hub/README.md) |
| [Teach](skills/teach/) | Research-backed, illustrated standalone HTML explainers with light and dark themes that grow as related questions are added. Informal by design, with no quizzes, progress tracking, or course mechanics. | [README](skills/teach/README.md) |

## Install

Install a specific skill with the [skills CLI](https://skills.sh/docs/cli):

```bash
npx skills@latest add AshishSalaskar1/skills --skill memory-hub
```

Review a skill's directory and documentation before installing it. Additional skills will be listed here as the collection grows.

## Repository Structure

```text
skills/
|-- memory-hub/
|   |-- SKILL.md
|   |-- README.md
|   |-- assets/
|   |-- references/
|   `-- scripts/
`-- teach/
    |-- SKILL.md
    |-- README.md
    `-- references/
```

`SKILL.md` is the agent-facing entry point for each skill. A skill's `README.md` is human-facing documentation for browsing the repository and is not part of the skill's runtime instructions.

## Development

Tests and validation commands are documented in each skill's README. Run the Memory Hub suite from the repository root with:

```bash
python3 -m unittest discover -s tests -v
```

## License

[MIT](LICENSE)
