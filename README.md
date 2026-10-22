# dev-templates

Reusable project templates for personal development, powered by [Copier](https://copier.readthedocs.io/).

## Templates

- [python-cli](./python-cli/) — Python CLI starter using `uv`, `pytest`, Ruff, a `src/` layout, VS Code Dev Containers, and GitHub Actions.

## Generate a project

Install Copier:

```bash
pipx install copier
```

Generate a project from this repository:

```bash
copier copy gh:asher-tian/dev-templates/python-cli ./my-cli
```

Then enter the generated project and run:

```bash
cd my-cli
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

Templates should stay focused. Add infrastructure such as Redis or PostgreSQL only to templates that require it.
