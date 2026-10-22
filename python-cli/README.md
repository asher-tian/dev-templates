# Python CLI template

Copier template for a small Python CLI project using:

- `uv` for Python environments and dependency management
- `pytest` for tests
- Ruff for linting and formatting
- A `src/` package layout
- VS Code Dev Containers (optional)
- GitHub Actions CI

## Generate

From any directory:

```bash
copier copy gh:asher-tian/dev-templates/python-cli ./my-cli
```

The template asks for the project name, Python package name, and Python version. After generation:

```bash
cd my-cli
uv sync --all-groups
uv run pytest
uv run ruff check .
uv run ruff format --check .
```

The CLI template stays intentionally minimal. Add Redis, databases, or other services to a separate template only when they are required.
