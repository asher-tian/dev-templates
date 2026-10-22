# Agent instructions

## Project conventions

- Use `uv` for Python environment and dependency management. Do not install project dependencies globally.
- Keep runtime dependencies in `[project].dependencies` and development tools in the `dev` dependency group.
- Preserve the `src/` layout.
- Keep `pyproject.toml` and `uv.lock` consistent; commit both.
- Do not add dependencies unless needed; explain why when adding one.
- Never commit `.env` files, tokens, passwords, private keys, or other secrets.

## Before finishing a change

Run:

```bash
uv run ruff check .
uv run ruff format --check .
uv run pytest
```

If a command cannot run, report the reason rather than claiming it passed.
