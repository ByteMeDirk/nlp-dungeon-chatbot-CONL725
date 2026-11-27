# nlp-dungeon-chatbot-CONL725

CONL725 NLP Chat Bot Assignment codebase: `dmbot`, a dungeon master chatbot.

## Stack

PyTorch, NLTK, Textual (TUI), Pydantic, SQLModel (SQLite ORM), PyYAML.
Tooling: uv, ruff, pyright, pytest, Trunk.

## Setup

```bash
uv sync
trunk git-hooks sync   # install the Trunk pre-commit/pre-push hooks
```

## Pipelines

Pipelines are ordered lists of steps in `pipelines.yaml`. Each step is a
`package.module:function` reference to a zero-argument callable.

```bash
uv run dmbot list            # show pipelines
uv run dmbot run extract     # create SQLite schema + download NLTK data
uv run dmbot run launch      # extract, then start the TUI
uv run dmbot-launch          # shortcut for the line above
uv run dmbot-extract         # shortcut for `dmbot run extract`
```

To add a pipeline, write a step function under `src/dmbot/steps/`, list it in
`pipelines.yaml`, and (optionally) add a `[project.scripts]` shortcut in
`pyproject.toml`.

Runtime data lives in `data/` (override with `DMBOT_DATA_DIR`).

## Quality checks

```bash
uv run ruff format . && uv run ruff check .
uv run pyright
uv run pytest
trunk check --all
```
